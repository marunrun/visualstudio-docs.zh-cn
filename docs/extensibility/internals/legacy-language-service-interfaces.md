---
title: 传统语言服务接口 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IVsLanguageInfo interface
- language services, objects
ms.assetid: 03b2d507-f463-417e-bc22-bdac68eeda52
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 89d80d6961f5eaf91721567ccb0efa73bbe31406
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707388"
---
# <a name="legacy-language-service-interfaces"></a>旧版语言服务接口
对于任何特定的编程语言，一次只能有一个语言服务的实例。 但是，单一语言服务可以服务多个编辑器。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]不将语言服务与任何特定编辑器相关联。 因此，当您请求语言服务操作时，必须将适当的编辑器标识为参数。

## <a name="common-interfaces-associated-with-language-services"></a>与语言服务关联的通用接口
 编辑器通过调用<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>相应的 VSPackage 获得您的语言服务。 在此调用中传递的服务 ID （SID） 标识要请求的语言服务。

 您可以在任意数量的单独类上实现核心语言服务接口。 但是，一种常见方法是在单个类中实现以下接口：

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageBlock>（可选）

  接口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>必须在所有语言服务上实现。 它提供有关语言服务的信息，例如语言的本地化名称、与语言服务关联的文件名扩展名以及如何检索着色器。

## <a name="additional-language-service-interfaces"></a>其他语言服务接口
 您的语言服务可以提供其他接口。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]请求这些接口的单独实例，用于文本缓冲区的每个实例。 因此，您应该在自己的对象上实现每个接口。 下表显示了每个文本缓冲区实例需要一个实例的接口。

|接口|描述|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|管理代码窗口修饰，如下拉栏。 您可以使用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A>方法获取此接口。 每个代码窗口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>有一个窗口。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>|着色语言关键字和分隔符。 您可以使用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>方法获取此接口。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>在绘制时调用。 避免计算密集型工作，<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>否则性能可能会受到影响。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>|提供 IntelliSense 参数工具提示。 当语言服务识别指示应显示方法数据的字符（如打开的括号）时，它将调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A>方法通知文本视图语言服务已准备好显示参数信息工具提示。 然后，文本视图使用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>接口的方法调用语言服务以获取显示工具提示所需的信息。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>|提供 IntelliSense 语句完成。 当语言服务准备好显示完成列表时，它将调用文本视图上<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>的方法。 然后，文本视图使用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>对象上的方法调用回语言服务。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>|允许使用命令处理程序修改文本视图。 实现接口的<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>类还必须实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口。 文本视图通过查询传递到<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter><xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget><xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>方法的对象来检索对象。 每个视图应该有一<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>个对象。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|拦截用户键入的代码窗口中的命令。 监视<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>实现输出，提供自定义完成信息和查看修改<br /><br /> 要将<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>对象传递到文本视图，请调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>。|

## <a name="see-also"></a>请参阅
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
- [清单：创建旧版语言服务](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)
