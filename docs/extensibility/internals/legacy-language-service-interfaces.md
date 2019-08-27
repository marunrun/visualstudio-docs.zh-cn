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
ms.openlocfilehash: 3a626111fc1f2eb8790cdfe2a146f63eba7fbab3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333490"
---
# <a name="legacy-language-service-interfaces"></a>旧版语言服务接口
对于任何特定的编程语言，可以有语言服务的一个实例一次。 但是，单一语言服务可以提供多个编辑器。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 不会将语言服务关联的任何特定的编辑器。 因此，当请求的语言服务操作时，必须作为参数确定适当的编辑器。

## <a name="common-interfaces-associated-with-language-services"></a>语言服务关联的公共接口
 在编辑器通过调用来获取你的语言服务<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>上相应的 VSPackage。 此调用中传递 ID (SID) 的服务标识所请求的语言服务。

 可以在任意数量的单独的类上实现核心语言服务接口。 但是，常见方法是在单个类中实现以下接口：

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageBlock> （可选）

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>接口必须实现所有的语言服务。 它提供有关你的语言服务，如语言，与语言服务，以及如何检索着色器关联的文件扩展名的本地化名称的信息。

## <a name="additional-language-service-interfaces"></a>另一种语言服务接口
 其他接口可以提供与你的语言服务。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 请求这些接口的文本缓冲区的每个实例的单独实例。 因此，您应实现这些接口的每个在其自己的对象上。 下表显示了需要每个文本缓冲区实例的一个实例的接口。

|接口|描述|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|管理代码窗口修饰，如下拉栏。 可以通过使用来获取此接口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A>方法。 还有一个<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>每个代码窗口。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>|用于控制语言关键字和分隔符。 可以通过使用来获取此接口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>方法。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 在绘制时调用。 避免在计算密集型工作<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>或性能可能会受到影响。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>|提供了 IntelliSense 参数工具提示。 当语言服务识别出的字符，该值指示该方法的数据应是显示，例如左括号，它将调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A>方法以通知文本的视图，语言服务已准备好显示的参数信息工具提示。 文本视图然后回调到语言服务由使用的方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>接口，用于获取所需的信息以显示工具提示。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>|提供了 IntelliSense 语句完成。 当语言服务已准备好显示完成列表时，它将调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>文本视图上的方法。 文本视图然后回调到语言服务的使用方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>对象。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>|允许修改文本视图使用的命令处理程序。 在其中您实现的类<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>接口还必须实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口。 文本视图检索<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>通过查询对象<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>对象传递到<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>方法。 应有一个<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>为每个视图的对象。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|截获命令在用户键入到代码窗口。 监视输出你<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>实现，以提供自定义完成信息并查看修改<br /><br /> 要传递你<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>对象的文本视图中，调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>。|

## <a name="see-also"></a>请参阅
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
- [清单：创建旧版语言服务](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)