---
title: 旧版语言服务接口 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80707388"
---
# <a name="legacy-language-service-interfaces"></a>旧版语言服务接口
对于任何特定的编程语言，一次只能有一个语言服务的实例。 不过，一种语言服务可为多个编辑器提供服务。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 不将语言服务与任何特定编辑器相关联。 因此，当您请求语言服务操作时，必须将相应的编辑器标识为参数。

## <a name="common-interfaces-associated-with-language-services"></a>与语言服务关联的通用接口
 编辑器通过 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> 在相应的 VSPackage 上调用来获取您的语言服务。 在此调用中传递的服务 ID (SID) 用于标识所请求的语言服务。

 可在任意数量的单独类上实现核心语言服务接口。 不过，一种常见方法是在单一类中实现以下接口：

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageBlock>（可选）

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>接口必须在所有语言服务上实现。 其中提供了有关语言服务的信息，例如语言的本地化名称、与语言服务关联的文件扩展名以及如何检索 colorizer。

## <a name="additional-language-service-interfaces"></a>其他语言服务接口
 其他接口可与你的语言服务一起提供。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 为文本缓冲区的每个实例请求这些接口的单独实例。 因此，应在其自己的对象上实现每个接口。 下表显示了每个文本缓冲区实例需要一个实例的接口。

|接口|说明|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|管理代码窗口装饰，如下拉栏。 可以使用方法获取此接口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> 。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>每个代码窗口都有一个。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>|着色语言关键字和分隔符。 可以使用方法获取此接口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> 。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 在绘制时调用。 避免计算密集型工作发生 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> ，或性能可能会降低。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>|提供 IntelliSense 参数工具提示。 当语言服务识别到指示应显示方法数据的字符（如左括号）时，它会调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> 方法，通知文本视图语言服务已准备好显示参数信息工具提示。 文本视图通过使用接口的方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> 来获取显示工具提示所需的信息，从而回叫语言服务。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>|提供 IntelliSense 语句完成。 当语言服务准备好显示完成列表时，它会 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> 在文本视图上调用方法。 然后，文本视图使用对象上的方法回调到语言服务 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> 。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>|允许使用命令处理程序修改文本视图。 实现接口的类 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> 还必须实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口。 文本视图 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> 通过查询 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 传递给方法的对象来检索对象 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> 。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>每个视图都应有一个对象。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|截获用户在代码窗口中键入的命令。 监视你的实现的输出 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ，以提供自定义完成信息和查看修改<br /><br /> 若要将您 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 的对象传递给文本视图，请调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> 。|

## <a name="see-also"></a>另请参阅
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
- [清单：创建旧版语言服务](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)
