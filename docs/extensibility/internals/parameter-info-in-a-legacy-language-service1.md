---
title: 旧语言服务中的参数信息1 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, method tips
- method tips
- language services, parameter info tooltip
- IVsMethodData interface
- Parameter Info (IntelliSense)
ms.assetid: f367295e-45b6-45d2-9ec8-77481743beef
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c26073252aae5434ba5a8197955948d0d9ec883d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706792"
---
# <a name="parameter-info-in-a-legacy-language-service"></a>旧版语言服务中的参数信息
IntelliSense 参数信息工具提示为用户提供有关他们在语言构造中位置的提示。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解更多信息，请参阅[扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

## <a name="how-parameter-info-tooltips-work"></a>参数信息工具提示的工作原理
 在编辑器中键入语句时，VSPackage 将显示一个小工具提示窗口，其中包含要键入的语句的定义。 例如，如果键入 Microsoft 基础类 （MFC） 语句（如`pMainFrame ->UpdateWindow`），然后按打开括号键开始列出参数，则会出现一个方法提示，显示`UpdateWindow`方法的定义。

 参数信息工具提示通常与语句完成一起使用。 它们对于在方法名称或关键字之后具有参数或其他格式化信息的语言最有用。

 参数信息工具提示由语言服务通过命令拦截启动。 要拦截<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>用户字符，语言服务对象必须实现接口，并通过在接口中调用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget><xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>方法，将文本视图传递给实现。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 命令筛选器拦截您在代码窗口中键入的命令。 监视命令信息，了解何时向用户显示参数信息。 可以使用相同的命令筛选器进行语句完成、错误标记等。

 当您键入语言服务可以提供提示的关键字时，语言服务将创建一个<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow>对象，并在<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A><xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>界面中调用方法通知 IDE 显示提示。 使用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow>`VSLocalCreateInstance`和 指定共类`CLSID_VsMethodTipWindow`创建对象。 `VsLocalCreateInstance`是在标头文件 vsdoc.h 中定义的函数，用于`QueryService`调用本地注册表并调用`CreateInstance`此对象。 `CLSID_VsMethodTipWindow`

## <a name="providing-a-method-tip"></a>提供方法提示
 要提供方法提示，请调用接口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A>中<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow>的方法，将其传递给接口的<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>实现。

 调用类<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>时，其方法按以下顺序调用：

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetContextStream%2A>

     返回当前文本缓冲区中相关数据的位置和长度。 这指示 IDE 不要使用工具提示窗口遮盖该数据。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetCurMethod%2A>

     返回要最初显示的方法编号（零基索引）。 例如，如果返回零，则最初显示第一个重载方法。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetOverloadCount%2A>

     返回适用于当前上下文的重载方法的数量。 如果为此方法返回大于 1 的值，则文本视图将显示向上和向下的箭头。 如果单击向下箭头，IDE 将调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.NextMethod%2A>方法。 如果单击向上箭头，IDE 将调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.PrevMethod%2A>方法。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A>

     参数信息工具提示的文本是在对 和 方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A><xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A>的多次调用期间构造的。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterCount%2A>

     返回要在方法中显示的参数数。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A>

     如果返回与要显示的重载对应的方法编号，则调用此方法，然后调用 方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A>。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A>

     在显示方法提示时，通知语言服务更新编辑器。 在<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A>方法中，调用以下内容：

    ```
    <pTxWin> ->UpdateTipWindow(<pTip>, UTW_CONTENTCHANGED | UTW_CONTEXTCHANGED).
    ```

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>

     关闭方法提示窗口时，<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>会收到对 方法的调用。
