---
title: 适用于语言的重要命令服务筛选器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, filters
- language services, commands to support
ms.assetid: 4948c494-3d4d-4f50-b3f9-959e73f90e4d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 73ecbad3578c356ed9f82f79cdf9144d4c2bd32d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66335075"
---
# <a name="important-commands-for-language-service-filters"></a>语言服务筛选器的重要命令
如果你想要创建一个全功能的语言服务筛选器，请考虑处理以下的命令。 在中定义的命令标识符的完整列表<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>非托管枚举为托管的代码和 Stdidcmd.h 标头文件[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]代码。 您可以找到 Stdidcmd.h 文件中的*Visual Studio SDK 安装路径*\VisualStudioIntegration\Common\Inc。

## <a name="commands-to-handle"></a>句柄的命令

> [!NOTE]
> 不一定要筛选的下表中的每个命令。

|命令|描述|
|-------------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|当用户单击鼠标右键时发送。 此命令指示，是时候提供快捷菜单。 如果不处理此命令，请在文本编辑器提供了默认的快捷菜单，而无需任何特定于语言的命令。 若要包含在此菜单上的命令，处理命令，并自行显示快捷菜单。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|当用户键入 CTRL + J 时，通常发送。 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>显示语句完成框。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|当用户键入字符时发送。 监视以确定何时键入触发器字符和提供语句完成、 方法提示和文本标记，如语法着色，大括号匹配，此命令和错误标记。 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>以完成语句和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A>方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow>方法提示和技巧。 若要支持文本标记，监视此命令，以确定是否在键入的字符，你需要更新您的标记。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|当用户键入 Enter 键时发送。 监视此命令，以确定何时关闭方法提示窗口，通过调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>。 默认情况下，文本视图处理此命令。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|当用户键入 Backspace 键时发送。 监视以确定何时将通过调用取消方法提示窗口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>。 默认情况下，文本视图处理此命令。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|从菜单或快捷键发送。 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A>方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>若要使用的参数信息更新提示窗口。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|当用户悬停在变量或将光标置于变量上，选择时发送**快速信息**从**IntelliSense**中**编辑**菜单。 在提示中的变量的类型返回通过调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A>方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>。 如果调试处于活动状态，该提示也应显示变量的值。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|当用户键入 CTRL + 空格键时，通常发送。 此命令指示要调用的语言服务<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID><br /><br /> <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|从菜单中，通常发送**注释选定内容**或**取消注释选定内容**从**高级**中**编辑**菜单。 <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> 指示用户想要注释掉所选的文本;<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>指示用户想要取消注释所选的文本。 这些命令可以仅由语言服务实现。|

## <a name="see-also"></a>请参阅
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)