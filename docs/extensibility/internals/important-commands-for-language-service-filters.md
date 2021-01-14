---
title: 语言服务筛选器的重要命令 |Microsoft Docs
description: 了解在 Visual Studio 中创建功能完备的语言服务筛选器时应支持的重要命令。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, filters
- language services, commands to support
ms.assetid: 4948c494-3d4d-4f50-b3f9-959e73f90e4d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 13014d61450897897029750b012833cf93a57729
ms.sourcegitcommit: a436ba564717b992eb1984b28ea0aec801eacaec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98204613"
---
# <a name="important-commands-for-language-service-filters"></a>语言服务筛选器的重要命令
如果要创建功能齐全的语言服务筛选器，请考虑处理以下命令。 命令标识符的完整列表在 <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> 托管代码的枚举和非托管代码的 Stdidcmd 头文件中定义 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 。 可在 *Visual STUDIO SDK 安装路径*\VisualStudioIntegration\Common\Inc. 中找到 Stdidcmd 文件。

## <a name="commands-to-handle"></a>要处理的命令

> [!NOTE]
> 不强制筛选下表中的每个命令。

|命令|描述|
|-------------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|当用户单击鼠标右键时发送。 此命令指示提供快捷菜单的时间。 如果不处理此命令，文本编辑器会提供默认快捷菜单，没有任何特定于语言的命令。 若要在此菜单中包含自己的命令，请自行处理命令并显示快捷菜单。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|通常在用户键入 CTRL + J 时发送。 对调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> 方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 以显示语句完成框。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|用户键入字符时发送。 监视此命令以确定何时键入触发器字符并提供语句完成、方法提示和文本标记，如语法着色、大括号匹配和错误标记。 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> 上的方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 以完成语句，并在上调用方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> 提示。 若要支持文本标记，请监视此命令以确定要键入的字符是否要求您更新标记。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|用户键入 Enter 键时发送。 监视此命令可通过对调用方法来确定何时消除方法提示窗口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> 。 默认情况下，文本视图将处理此命令。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|用户键入 Backspace 键时发送。 通过在上调用方法来确定何时消除方法提示窗口的监视器 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> 。 默认情况下，文本视图将处理此命令。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|从菜单或快捷键发送。 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> 上的方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ，以更新带有参数信息的提示窗口。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|当用户将鼠标指针悬停在某个变量上，或将光标置于变量上，并从 "**编辑**" 菜单中的 **IntelliSense** 中选择 "**快速信息**" 时发送。 通过对调用方法，在 tip 中返回变量的类型 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。 如果调试处于活动状态，则提示还应显示变量的值。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|通常在用户键入 CTRL + 空格键时发送。 此命令告知语言服务在 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> 上调用方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID><br /><br /> <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|从菜单中发送，通常是在 "**编辑**" 菜单中的 "高级"**选项****或 "** **高级**"。 <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> 指示用户要注释掉所选文本; <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> 指示用户要取消对所选文本的注释。 这些命令只能由语言服务实现。|

## <a name="see-also"></a>另请参阅
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
