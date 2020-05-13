---
title: 语言服务筛选器的重要命令 |微软文档
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
ms.openlocfilehash: bb29ee5b5a5359d6cfe34911656dfe9be015262e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707616"
---
# <a name="important-commands-for-language-service-filters"></a>语言服务筛选器的重要命令
如果要创建功能齐全的语言服务筛选器，请考虑处理以下命令。 命令标识符的完整列表在托管代码的<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>枚举和非托管[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]代码的 Stdidcmd.h 标头文件中定义。 您可以在*Visual Studio SDK 安装路径*[VisualStudio 集成]公共_Inc 中找到 Stdidcmd.h 文件。

## <a name="commands-to-handle"></a>要处理的命令

> [!NOTE]
> 不必对下表中的每个命令进行筛选。

|命令|描述|
|-------------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|用户右键单击时发送。 此命令指示是时候提供快捷菜单了。 如果不处理此命令，文本编辑器提供默认快捷菜单，而不执行任何特定于语言的命令。 要在此菜单上包含您自己的命令，请自行处理该命令并显示快捷菜单。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|通常在用户键入 CTRL_J 时发送。 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>上的方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>以显示语句完成框。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|在用户键入字符时发送。 监视此命令以确定何时键入触发器字符，并提供语句完成、方法提示和文本标记，如语法着色、大括号匹配和错误标记。 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A><xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>for 语句完成上<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A>的方法和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow>for 方法提示上的方法。 要支持文本标记，请监视此命令以确定键入的字符是否需要更新标记。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|在用户键入 Enter 键时发送。 监视此命令，通过在 上调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>方法来确定何时关闭方法提示窗口。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> 默认情况下，文本视图处理此命令。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|在用户键入"后空间"键时发送。 监视，通过在 上调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>方法来确定何时关闭方法提示窗口。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> 默认情况下，文本视图处理此命令。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|从菜单或快捷键发送。 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A>上的方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>以使用参数信息更新提示窗口。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|当用户悬停在变量上或将光标定位在变量上，并在 **"编辑"** 菜单中选择"IntelliSense"中的**IntelliSense****"快速信息**"时，已发送。 通过在 调用 上 的方法返回<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A>提示中的变量的类型。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 如果调试处于活动状态，则提示还应显示变量的值。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|通常在用户键入 CTRL_空格键时发送。 此命令告诉语言服务调用 上<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>的方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID><br /><br /> <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|从菜单发送，通常是 **"编辑"** 菜单中的 **"高级"中的"注释选择**"或 **"取消注释选择**"。 **Advanced** <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>指示用户要注释掉所选文本;但<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>指示用户要取消注释所选文本。 这些命令只能由语言服务实现。|

## <a name="see-also"></a>请参阅
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
