---
title: 旧版语言服务 1 中的参数信息 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, method tips
- method tips
- language services, parameter info tooltip
- IVsMethodData interface
- Parameter Info (IntelliSense)
ms.assetid: f367295e-45b6-45d2-9ec8-77481743beef
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5b1707313c40e7ea720fff3b9f70546af00ea486
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63408654"
---
# <a name="parameter-info-in-a-legacy-language-service"></a>旧版语言服务中的参数信息
参数的 IntelliSense 信息工具提示为用户提供有关其所在的语言构造中的提示。

 旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要获取详细信息，请参阅[扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 我们建议在开始尽可能快地使用新编辑器 API。 这将提高您的语言服务的性能，让您充分利用新的编辑器功能。

## <a name="how-parameter-info-tooltips-work"></a>参数信息工具提示的工作原理
 当在编辑器中键入一条语句时，VSPackage 将显示包含所键入的语句定义的小工具提示窗口。 例如，如果键入 Microsoft 基础类 (MFC) 语句 (如`pMainFrame ->UpdateWindow`) 和按左括号键用于开始列出的参数，将显示的方法提示，显示的定义`UpdateWindow`方法。

 参数信息工具提示通常是与语句完成结合使用。 它们是最适用于具有参数或其他方法名称或关键字后的格式化的信息的语言。

 参数信息工具提示是通过命令拦截语言服务启动的。 若要截获用户字符，您的语言服务对象必须实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口，并将文本视图传递一个指向您<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>实现中的，通过调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>中的方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>接口。 命令筛选器会截获到代码窗口中键入的命令。 监视命令信息以了解何时向用户显示参数信息。 用于语句完成、 错误标记等，可以使用的相同命令筛选器。

 当键入的关键字的语言服务可以为其提供提示时，然后该语言服务将创建<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow>对象并调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A>中的方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>接口以通知 IDE 以显示一个提示。 创建<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow>对象使用`VSLocalCreateInstance`并指定组件类`CLSID_VsMethodTipWindow`。 `VsLocalCreateInstance` 是一个函数定义中调用标头文件 vsdoc.h`QueryService`本地注册表和调用`CreateInstance`此对象上`CLSID_VsMethodTipWindow`。

## <a name="providing-a-method-tip"></a>提供方法提示
 若要提供方法提示，请调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A>中的方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow>接口，并向其传递的实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>接口。

 当你<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>调用类中，按以下顺序调用其方法：

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetContextStream%2A>

     返回当前文本缓冲区中的位置和相关数据的长度。 这会指示 IDE 不会影响该数据与工具提示窗口。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetCurMethod%2A>

     返回方法数 （从零开始的索引），你想要一开始显示。 例如，如果返回零，则第一个重载的方法最初呈现。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetOverloadCount%2A>

     返回当前上下文中适用的重载方法的数量。 如果返回值大于 1 的此方法，然后在文本视图显示向上和向下箭头。 如果您单击向下箭头，IDE 会调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.NextMethod%2A>方法。 如果单击向上箭头时，IDE 会调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.PrevMethod%2A>方法。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A>

     在多次调用过程中构造参数信息工具提示的文本<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A>和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A>方法。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterCount%2A>

     返回要显示的方法中的参数数目。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A>

     如果返回想要显示的重载与相对应的方法数字时，调用此方法，调用后跟<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A>方法。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A>

     通知语言服务以更新编辑器时显示方法提示。 在<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A>方法，调用以下命令：

    ```
    <pTxWin> ->UpdateTipWindow(<pTip>, UTW_CONTENTCHANGED | UTW_CONTEXTCHANGED).
    ```

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>

     接收到调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>方法时关闭方法提示窗口。