---
title: 选项，文本编辑器，C#，IntelliSense | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Intellisense
- VS.ToolsOptionsPages.Text_Editor.Visual_JSharp.Intellisense
helpviewer_keywords:
- IntelliSense [J#], options
- underlines, wavy
- IntelliSense [C#], options
- IntelliSense [C#], wavy underlines
- wavy underlines
- Text Editor Options dialog box, IntelliSense
ms.assetid: 3466dedb-e5f4-424c-8dd8-e4941b2f4fc2
caps.latest.revision: 30
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1e3f4df9a7a885245e40f7e9fec1b0da207ada39
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662297"
---
# <a name="options-text-editor-c-intellisense"></a>选项，文本编辑器，C#，IntelliSense
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用“IntelliSense”  属性页可以修改影响 IntelliSense for Visual C# 行为的设置。 通过单击“工具”  菜单上的“选项”  ，再单击“文本编辑器”  文件夹中的“C#”  ，然后单击“IntelliSense”  ，可以访问“IntelliSense”  属性页。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。

 “IntelliSense”  属性页包含下列属性：

## <a name="completion-lists"></a>完成列表
 **键入字符后显示完成列表**如果选择此选项，则在开始键入时，IntelliSense 会自动显示完成列表。 未选择此选项时，仍可从“IntelliSense”  菜单或通过按 Ctrl+空格来使用 IntelliSense 完成功能。

 **将关键字放入完成列表**选中此选项后，IntelliSense 将关键字C# （例如[class](https://msdn.microsoft.com/library/b95d8815-de18-4c3f-a8cc-a0a53bdf8690)）添加到完成列表。

 **将代码片段放入完成列表**选中此选项后，IntelliSense 会将代码片段C#的别名添加到完成列表。 如果代码片段别名与关键字相同（例如均为 [class](https://msdn.microsoft.com/library/b95d8815-de18-4c3f-a8cc-a0a53bdf8690)），则快捷方式将替代关键字。 有关详细信息，请参阅 [Visual C#代码片段](../../ide/visual-csharp-code-snippets.md)。

## <a name="selection-in-completion-lists"></a>完成列表中的选定内容
 **通过键入以下字符提交：** 指定在键入完成列表中的选定项后对其执行 IntelliSense 自动完成的所有字符。

 **按空格键提交**指定包含按空格键执行完成列表中选定项的 IntelliSense 自动完成的操作。

 在**完整键入的单词末尾添加输入新行**指定在完成列表中键入条目的所有字符，然后按 ENTER，将自动创建一个新行，并将光标移动到新行。

 例如，如果键入 `else` 后按 Enter，则编辑器中显示以下内容：

 `else`

 `|`（光标位置）

 但是，如果仅键入 `el`，然后按 Enter，则编辑器中显示以下内容：

 `else|`（光标位置）

## <a name="intellisense-member-selection"></a>IntelliSense 成员选择
 **预先选择最近使用**过的成员选中此选项后，IntelliSense 将预先选择在集成开发环境（IDE）中的当前会话期间，你最近在弹出列表 "成员" 框中选择的成员，以自动完成对象名称。 在 IDE 中的每个会话之间，最近使用过的成员的历史记录将被清除。 有关详细信息，请参阅[用于最近使用过的成员的 IntelliSense](../../misc/intellisense-for-most-recently-used-members.md)

## <a name="see-also"></a>另请参阅
 ["常规"、"环境"、"选项" 对话框](../../ide/reference/general-environment-options-dialog-box.md) [XML 文档注释](https://msdn.microsoft.com/library/803b7f7b-7428-4725-b5db-9a6cff273199)[使用 IntelliSense](../../ide/using-intellisense.md)
