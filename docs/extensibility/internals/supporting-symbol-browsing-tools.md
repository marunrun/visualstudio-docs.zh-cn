---
title: 支持符号浏览工具 |微软文档
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
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4998e47ccd6f99df2710833c18975d57e3bb92f5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704770"
---
# <a name="supporting-symbol-browsing-tools"></a>支持符号浏览工具
**对象浏览器**、**类视图**、**调用浏览器**和**查找符号结果**工具在可视化工作室中提供符号浏览功能。 这些工具显示符号的分层树视图，并显示树中符号之间的关系。 符号可以表示命名空间、对象、类、类成员和各种组件中包含的其他语言元素。 这些组件包括 Visual Studio 项目、外部 .NET 框架组件和类型 （.tlb） 库。 有关详细信息，请参阅[查看代码的结构](../../ide/viewing-the-structure-of-code.md)。

## <a name="symbol-browsing-libraries"></a>符号浏览库
 作为语言实现者，您可以通过创建跟踪组件中的符号的库，并通过一组接口向 Visual Studio 对象管理器提供符号列表来扩展 Visual Studio 符号浏览功能。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2>接口描述了库。 Visual Studio 对象管理器通过从库中获取数据并组织数据来响应从符号浏览工具中获取新数据的请求。 随后，它将使用请求的数据填充或更新工具。 要获取对 Visual Studio 对象管理器的<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2>引用，将<xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager>服务 ID`GetService`传递给 方法。

 每个库都必须向 Visual Studio 对象管理器注册，该管理器收集所有库的信息。 要注册库，请调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A>方法。 根据启动请求的工具，Visual Studio 对象管理器会查找相应的库并请求数据。 数据在<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2>接口描述的符号列表中在库和[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]对象管理器之间传输。

 对象[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]管理器负责定期刷新符号浏览工具，以反映库中包含的最最新数据。

 下图包含库和 Visual Studio 对象管理器之间的请求/数据交换过程的关键元素示例。 关系图中的接口是托管代码应用程序的一部分。

 ![库与对象管理器间的数据流](../../extensibility/internals/media/callbrowserdiagram.gif "呼叫浏览器图")

 要向 Visual Studio 对象管理器提供符号列表，必须首先通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A>方法将库注册到 Visual Studio 对象管理器。 注册库后，Visual Studio 对象管理器会请求有关库功能的某些信息。 例如，它通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetLibFlags2%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetSupportedCategoryFields2%2A>方法请求库标志和支持的类别。 在某些时候，当其中一个工具请求来自此库的数据时，对象管理器通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetList2%2A>方法请求符号的顶级列表。 作为回应，库会创建符号列表，并通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2>接口将其公开给 Visual Studio 对象管理器。 对象[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]管理器通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetItemCount%2A>方法确定列表中有多少项。 以下所有请求都与列表中的给定项相关，并在每个请求中提供物料索引编号。 Visual Studio 对象管理器继续通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetCategoryField2%2A>方法收集有关项的类型、可访问性和其他属性的信息。

 它通过调用 方法确定项的名称，<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetTextWithOwnership%2A>并通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetDisplayData%2A>方法请求图标信息。 图标显示在项目名称的左侧，并描述项的类型、辅助功能和其他属性。

 对象[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]管理器调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetExpandable3%2A>方法以确定给定列表项是否可展开，并且具有子项。 如果 UI 发送扩展元素的请求，对象管理器通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetList2%2A>方法请求符号的子列表。 该过程继续，树的不同部分正在按需构建。

> [!NOTE]
> 要实现本机代码符号提供程序，请使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsLibrary2>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectList2>接口。

## <a name="see-also"></a>请参阅
- [如何：使用对象管理器注册库](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [如何：向对象管理器公开库提供的符号列表](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
- [如何：识别库中的符号](../../extensibility/internals/how-to-identify-symbols-in-a-library.md)
