---
title: 旧版语言 Service1 中的参数信息 |Microsoft Docs
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
ms.openlocfilehash: 8f8e5664634d189e8463376761d8fb59543740df
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238070"
---
# <a name="parameter-info-in-a-legacy-language-service-1"></a>旧版语言服务中的参数信息1
IntelliSense 参数信息工具提示向用户提供有关其在语言构造中的位置的提示。

 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解详细信息，请参阅 [扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。

## <a name="how-parameter-info-tooltips-work"></a>参数信息工具提示的工作方式
 当您在编辑器中键入语句时，VSPackage 会显示一个小的工具提示窗口，其中包含所键入的语句的定义。 例如，如果您在 MFC) 语句 (键入一个 Microsoft 基础类 (如 `pMainFrame ->UpdateWindow`) 并按下左括号键开始列出参数，则会出现一个方法提示，其中显示了该 `UpdateWindow` 方法的定义。

 参数信息工具提示通常与语句完成一起使用。 它们最适用于在方法名称或关键字后面包含参数或其他格式信息的语言。

 参数信息工具提示由语言服务通过命令截取启动。 若要截获用户字符，语言服务对象必须实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口，并 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 通过调用接口中的方法，将文本视图传递到实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。 命令筛选器会截获您在代码窗口中键入的命令。 监视命令信息以了解何时向用户显示参数信息。 您可以使用相同的命令筛选器来完成语句完成、错误标记等。

 键入语言服务可以为其提供提示的关键字时，语言服务将创建一个 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> 对象，并调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> 接口中的方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 以通知 IDE 显示提示。 使用创建 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> 对象 `VSLocalCreateInstance` 并指定 coclass `CLSID_VsMethodTipWindow` 。 `VsLocalCreateInstance` 是在标头文件 vsdoc 中定义的一个函数，该函数调用 `QueryService` 本地注册表并对 `CreateInstance` 的此对象调用 `CLSID_VsMethodTipWindow` 。

## <a name="providing-a-method-tip"></a>提供方法提示
 若要提供方法提示，请 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> 在接口中调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> 方法，并向其传递接口的实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> 。

 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>调用类时，将按以下顺序调用其方法：

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetContextStream%2A>

     返回当前文本缓冲区中相关数据的位置和长度。 这会指示 IDE 不会在工具提示窗口中隐藏该数据。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetCurMethod%2A>

     返回要最初显示的 (从零开始的索引) 的方法号。 例如，如果返回零，则最初将显示第一个重载方法。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetOverloadCount%2A>

     返回在当前上下文中适用的重载方法的数目。 如果为此方法返回一个大于1的值，则文本视图将显示您的上箭头和下箭头。 如果单击向下箭头，IDE 将调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.NextMethod%2A> 方法。 如果单击向上箭头，IDE 将调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.PrevMethod%2A> 方法。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A>

     参数信息工具提示的文本在多个对和方法的调用过程中构造 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A> 。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterCount%2A>

     返回要在方法中显示的参数的数目。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A>

     如果返回与要显示的重载对应的方法编号，则会调用此方法，然后调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A> 方法。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A>

     通知语言服务在显示方法提示时更新编辑器。 在 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A> 方法中，调用以下内容：

    ```
    <pTxWin> ->UpdateTipWindow(<pTip>, UTW_CONTENTCHANGED | UTW_CONTEXTCHANGED).
    ```

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>

     <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>关闭方法提示窗口时，会收到对方法的调用。
