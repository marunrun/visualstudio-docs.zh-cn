---
title: 选项，文本编辑器，所有语言，选项卡
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.All_Languages.Tabs
- VS.ToolsOptionsPages.Text_Editor.Basic.Tabs
- VS.ToolsOptionsPages.Text_Editor.CSharp.Tabs
- VS.ToolsOptionsPages.Text_Editor.C%2FC%2B%2B.Tabs
- VS.ToolsOptionsPages.Text_Editor.CoffeeScript.Tabs
- VS.ToolsOptionsPages.Text_Editor.CSS.Tabs
- VS.ToolsOptionsPages.Text_Editor.Dockerfile.Tabs
- VS.ToolsOptionsPages.Text_Editor.F%2523.Tabs
- VS.ToolsOptionsPages.Text_Editor.HQL.Tabs
- VS.ToolsOptionsPages.Text_Editor.HTML.Tabs
- VS.ToolsOptionsPages.Text_Editor.HTMLX.Tabs
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Tabs
- VS.ToolsOptionsPages.Text_Editor.TypeScript.Tabs
- VS.ToolsOptionsPages.Text_Editor.JSON.Tabs
- VS.ToolsOptionsPages.Text_Editor.LESS.Tabs
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.Tabs
- VS.ToolsOptionsPages.Text_Editor.ResJSON.Tabs
- VS.ToolsOptionsPages.Text_Editor.SCSS.Tabs
- VS.ToolsOptionsPages.Text_Editor.SQL_Server_Tools.Tabs
- VS.ToolsOptionsPages.Text_Editor.StreamAnalytics.Tabs
- VS.ToolsOptionsPages.Text_Editor.T-SQL90.Tabs
- VS.ToolsOptionsPages.Text_Editor.U-SQL.Tabs
- VS.ToolsOptionsPages.Text_Editor.XAML.Tabs
- VS.ToolsOptionsPages.Text_Editor.XML.Tabs
helpviewer_keywords:
- indents, Code Editor
- Code Editor, default behavior
- tabs, setting in Code Editor
- All Languages Text Editor Options dialog box
- editors, Code Editor
- Code Editor, indenting
- Code Editor, tabs
ms.assetid: 7e208e1d-5e3a-4bf7-a27b-4417e3e049c7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0fc169960cf757e4e334d5f77b06ff70b0d6da7c
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75594742"
---
# <a name="options-text-editor-all-languages-tabs"></a>选项，文本编辑器，所有语言，选项卡

使用此对话框可更改代码编辑器的默认行为。 这些设置也适用于其他基于代码编辑器的编辑器，如 HTML 设计器的“源”视图。 若要显示这些选项，请选择“工具”菜单中的“选项”   。 在“文本编辑器”中，展开“所有语言”子文件夹，然后选择“制表符”    。

> [!CAUTION]
> 在此页面用于设置所有开发语言的默认选项。 请记住，重置此对话框中的一个选项会将所有语言的“制表符”选项重置为在此处选择的任何选项。 若要只为一种语言更改文本编辑器选项，请展开该语言的子文件夹并选择其选项页。

如果在“制表符”选项页上为特定的编程语言选择了不同的设置，则对于不同的“缩进”选项，将显示消息“各种文本格式的缩进设置相互冲突”；对于不同的“制表符”选项，将显示消息“各种文本格式的制表符设置相互冲突”   。 例如，如果为 Visual Basic 选择了“智能缩进”选项，但为 Visual C++ 选择了“块缩进”，则会显示此提醒   。

## <a name="indenting"></a>缩进

无

选中后，新行不缩进。 插入点被置于新行的第一列。

块

选中后，新行自动缩进。 插入点被置于与上一行相同的起始点处。

智能

选中后，新行的放置依据开发语言的其他代码格式设置和 IntelliSense 约定，以适应代码上下文。 此选项并不是对所有开发语言都可用。

例如，括在左括号 ({) 和右括号 (}) 之间的行可能从对齐括号的位置自动缩进一个额外的制表位。

## <a name="tabs"></a>制表符

制表符大小

设置制表位之间的距离（以空格数表示）。 默认值为 4 个空格。

缩进大小

设置自动缩进的大小（以空格数表示）。 默认值为 4 个空格。 将插入制表符和/或空格字符来填充指定的大小。

插入空格

选中后，缩进操作只插入空格字符，而不插入制表符。 例如，如果“缩进大小”设置为 5，则每当按 Tab 键或单击“格式设置”工具栏上的“增加缩进”按钮时，都会插入五个空格字符    。

保留制表符

选中后，缩进操作会尽可能多地插入制表符。 每个制表符都会填充“制表符大小”中指定的空格数  。 如果“缩进大小”不是“制表符大小”的偶数倍，则会添加空格字符以填充差额   。

## <a name="see-also"></a>另请参阅

- [“选项”->“文本编辑器”->“所有语言”](../../ide/reference/options-text-editor-all-languages.md)
- [“选项”对话框 ->“环境”->“常规”](../../ide/reference/general-environment-options-dialog-box.md)
