---
title: 旧版语言服务接口 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IVsLanguageInfo interface
- language services, objects
ms.assetid: 03b2d507-f463-417e-bc22-bdac68eeda52
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 065ef972709ca78b516a9acc5f4a737d2963e4b7
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72726845"
---
# <a name="legacy-language-service-interfaces"></a>旧版语言服务接口
对于任何特定的编程语言，一次只能有一个语言服务的实例。 不过，一种语言服务可为多个编辑器提供服务。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 不会将语言服务与任何特定编辑器相关联。 因此，当您请求语言服务操作时，必须将相应的编辑器标识为参数。

## <a name="common-interfaces-associated-with-language-services"></a>与语言服务关联的通用接口
 编辑器通过在相应的 VSPackage 上调用 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> 来获取您的语言服务。 此调用中传递的服务 ID （SID）标识所请求的语言服务。

 可在任意数量的单独类上实现核心语言服务接口。 不过，一种常见方法是在单一类中实现以下接口：

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageBlock> （可选）

  必须在所有语言服务上实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> 接口。 其中提供了有关语言服务的信息，例如语言的本地化名称、与语言服务关联的文件扩展名以及如何检索 colorizer。

## <a name="additional-language-service-interfaces"></a>其他语言服务接口
 其他接口可与你的语言服务一起提供。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 为文本缓冲区的每个实例请求这些接口的单独实例。 因此，应在其自己的对象上实现每个接口。 下表显示了每个文本缓冲区实例需要一个实例的接口。

|接口|描述|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|管理代码窗口装饰，如下拉栏。 可以使用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> 方法获取此接口。 每个代码窗口有一个 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>|着色语言关键字和分隔符。 可以使用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> 方法获取此接口。 在绘制时调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>。 避免在 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 或性能可能降低的计算密集型工作。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>|提供 IntelliSense 参数工具提示。 当语言服务识别到指示应显示方法数据的字符（如左括号）时，它将调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> 方法，通知文本视图语言服务已准备好显示参数信息工具提示。 然后，文本视图使用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> 接口的方法返回到语言服务，以获取显示工具提示所需的信息。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>|提供 IntelliSense 语句完成。 当语言服务准备好显示完成列表时，它将对文本视图调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> 方法。 然后，文本视图使用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> 对象上的方法回调到语言服务。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>|允许使用命令处理程序修改文本视图。 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> 接口的类还必须实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口。 文本视图通过查询传入 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> 方法的 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 对象来检索 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> 的对象。 每个视图都应有一个 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> 对象。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|截获用户在代码窗口中键入的命令。 监视 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 实现的输出，以提供自定义完成信息和查看修改<br /><br /> 若要将 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 对象传递给文本视图，请调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>。|

## <a name="see-also"></a>请参阅
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
- [清单：创建旧版语言服务](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)