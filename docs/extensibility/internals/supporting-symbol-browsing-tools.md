---
title: 支持符号浏览工具 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- symbols, symbol-browsing tools
- browsers, symbol browsers
- symbol-browsing tools
- libraries
- IVsLibrary2 interface, symbol-browsing tools
- IVsSimpleLibrary2 interface, symbol-browsing tools
- symbol-browsing tools, library manager
- symbols
- libraries, symbol-browsing tools
ms.assetid: 70d8c9e5-4b0b-4a69-b3b3-90f36debe880
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a5e79969c3b4be22a3c9bb01f06297f54b0734ee
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66746011"
---
# <a name="supporting-symbol-browsing-tools"></a>支持符号浏览工具
**对象浏览器**，**类视图**，**调用浏览器**并**查找符号结果**工具提供浏览功能在 Visual Studio 中的符号。 这些工具显示的符号的层次结构树视图，并显示在树中的符号之间的关系。 符号可能代表命名空间、 对象、 类、 类成员和不同组件中包含其他语言元素。 这些组件包括 Visual Studio 项目、.NET Framework 的外部组件和类型 (.tlb) 库。 有关详细信息，请参阅[查看代码的结构](../../ide/viewing-the-structure-of-code.md)。

## <a name="symbol-browsing-libraries"></a>符号浏览库
 为语言实施者，可以通过创建跟踪您的组件中的符号，并向 Visual Studio 对象管理器通过一组接口提供的符号列表的库来扩展 Visual Studio 符号浏览功能。 描述一个库<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2>接口。 Visual Studio 对象管理器响应针对新数据的请求来自的符号浏览工具通过从库中获取数据并将其组织。 随后将填充，或使用所请求的数据更新工具。 若要获取对 Visual Studio 对象管理器中，引用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2>，传递<xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager>服务 ID 到`GetService`方法。

 每个库必须注册 Visual Studio 对象管理器，在所有库收集的信息。 若要注册一个库，请调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A>方法。 具体取决于哪种工具启动请求时，Visual Studio 对象管理器查找合适的库，并请求数据。 库之间传输数据并[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]符号所描述的列表中的对象管理器<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2>接口。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]对象管理器是负责定期刷新符号浏览工具，以反映最新的数据包含在库中。

 下图包含一个库和 Visual Studio 对象管理器之间的请求/数据交换过程中的主要元素的一个示例。 在关系图中的接口是托管的代码应用程序的一部分。

 ![一个库和对象管理器之间的数据流](../../extensibility/internals/media/callbrowserdiagram.gif "CallBrowserDiagram")

 若要向 Visual Studio 对象管理器提供的符号列表，必须先注册库与 Visual Studio 对象管理器通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A>方法。 注册了库后，Visual Studio 对象管理器请求的功能的库的某些信息。 例如，请求库标志，并通过调用支持类别<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetLibFlags2%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetSupportedCategoryFields2%2A>方法。 在某些时候，当一种工具请求数据从这个库中，对象管理器请求符号的顶级列表通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetList2%2A>方法。 在响应中，库制造符号的列表，并将它暴露给通过 Visual Studio 对象管理器<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2>接口。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]对象管理器确定通过调用列表中有多少项<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetItemCount%2A>方法。 下面的所有请求与给定项在列表中，并提供每个请求中的项索引号。 Visual Studio 对象管理器将继续收集的信息类型、 可访问性，以及其他项的属性通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetCategoryField2%2A>方法。

 它通过调用确定的项名称<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetTextWithOwnership%2A>方法，并通过调用请求图标信息<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetDisplayData%2A>方法。 图标显示左侧的项名称和描述了项目、 可访问性，其他属性的类型。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]对象管理器调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetExpandable3%2A>方法来确定给定的列表项是否可展开，并具有子级的项。 对象管理器 UI 发送请求以展开元素，如果通过调用请求符号的子列表<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetList2%2A>方法。 正在生成按需在树的不同部分继续。

> [!NOTE]
> 若要实现的本机代码符号提供程序，请使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsLibrary2>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectList2>接口。

## <a name="see-also"></a>请参阅
- [如何：使用对象管理器注册库](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [如何：向对象管理器公开库提供的符号列表](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
- [如何：识别库中的符号](../../extensibility/internals/how-to-identify-symbols-in-a-library.md)