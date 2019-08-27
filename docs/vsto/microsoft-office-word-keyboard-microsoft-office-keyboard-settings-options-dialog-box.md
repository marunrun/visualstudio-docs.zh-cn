---
title: Office Word 键盘，键盘设置选项对话框
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Microsoft_Office_Tools.Microsoft_Office_Word.Keyboard
- VS.ToolsOptionsPages.Microsoft_Office_Keyboard_Settings.Microsoft_Office_Word_Keyboard
- VST.WordOptions.KeyboardMappingScheme
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- keyboard shortcuts, Office development in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5180aa2f4c5022cedcba2c5377d2ff2ac14ffb28
ms.sourcegitcommit: cc5fd59e5dc99181601b7db8b28d7f8a83a36bab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2019
ms.locfileid: "66835983"
---
# <a name="microsoft-office-word-keyboard-microsoft-office-keyboard-settings-options-dialog-box"></a>Microsoft Office Word 键盘，Microsoft Office 键盘设置选项对话框
  Microsoft Office Word 和 Visual Studio 同时处理键盘快捷方式。 同一个快捷键组合可以代表不同的命令在 Word 中和 Visual Studio 中。 在 Visual Studio 中的文档级项目中打开 Word 时，一次只有一个应用程序接收的快捷键命令。 默认情况下，Visual Studio 接收所有快捷方式命令，但您可以使 Word 文档通过选择具有焦点时接收它们**动态键盘方案**。

 如果使用未分配给当前正在处理键盘快捷方式的应用程序中的命令的快捷键，快捷键被传递到其他应用程序。

 在更改之前，则你选择的选项将对 Word 项目仍然有效工作。 所选内容不会影响 Microsoft Office Excel 项目中;使用 Microsoft Office Excel 键盘选项，您必须使 excel 的任何更改。

## <a name="uielement-list"></a>UIElement 列表
 **Visual Studio 键盘方案**Visual Studio 接收所有快捷方式命令，即使该 Word 文档具有焦点。 例如，如果按功能键**F5**文档具有焦点，Visual Studio 将启动调试你的解决方案。

 **动态键盘方案**Visual Studio 仅具有焦点时接收的快捷键命令。 当 Word 文档具有焦点时，Word 将接收所有的快捷键命令。 例如，如果按功能键**F5** Word 文档具有焦点，则 Word 会打开**查找和替换**带有对话框**转到**选定的选项卡。 如果按下**F5**时 Visual Studio 具有焦点时，Visual Studio 将启动调试你的解决方案。

## <a name="see-also"></a>请参阅
- [Microsoft Office Excel 键盘，Microsoft Office 键盘设置选项对话框](../vsto/microsoft-office-excel-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)
