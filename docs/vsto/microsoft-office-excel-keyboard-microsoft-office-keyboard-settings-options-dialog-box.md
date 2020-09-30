---
title: Office Excel 键盘、"设置"、"选项" 对话框
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ExcelOptions.KeyboardMappingScheme
- VS.ToolsOptionsPages.Microsoft_Office_Keyboard_Settings.Microsoft_Office_Excel_Keyboard
- VS.ToolsOptionsPages.Microsoft_Office_Tools.Microsoft_Office_Excel.Keyboard
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
ms.openlocfilehash: 8b590f82d5f28c3a71e86e18dfe16b1c3e6c4c5a
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584511"
---
# <a name="microsoft-office-excel-keyboard-settings-options-dialog-box"></a>Microsoft Office Excel 键盘、"设置"、"选项" 对话框
  Microsoft Office Excel 和 Visual Studio 均处理快捷键。 在 Excel 和 Visual Studio 中，同一快捷键组合可用于不同的命令。 当在 Visual Studio 中的文档级项目中打开 Excel 时，一次只能有一个应用程序收到快捷键命令。 默认情况下，Visual Studio 会接收所有快捷键命令，但你可以通过选择 " **动态键盘方案**" 使 Excel 在文档具有焦点时接收它们。

 如果使用未分配给当前正在处理快捷键的应用程序中的命令的快捷键，则快捷键会传递到其他应用程序。

 你选择的选项将对 Excel 项目保持有效，直到你进行更改。 选择不会影响 Word 项目 Microsoft Office;您必须使用 Microsoft Office Word 键盘选项对 Word 进行任何更改。

## <a name="uielement-list"></a>UIElement 列表
 **Visual Studio 键盘方案** 即使 Excel 有焦点，Visual Studio 也会接收所有快捷键命令。 例如，如果在 Excel 有焦点时按 "函数键 **F5** "，则 Visual Studio 会开始调试解决方案。

 **动态键盘方案** Visual Studio 仅在其具有焦点时接收快捷键命令。 当 Excel 有焦点时，Excel 将接收所有快捷键命令。 例如，如果在 Excel 有焦点时按 "函数键 **F5** "，excel 将打开 " **转到** " 对话框。 如果你在 Visual Studio 有焦点的情况下按 **F5** ，visual studio 会开始调试你的解决方案。

## <a name="see-also"></a>另请参阅
- [Microsoft Office Word 键盘、Microsoft Office 键盘设置、"选项" 对话框](../vsto/microsoft-office-word-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)
