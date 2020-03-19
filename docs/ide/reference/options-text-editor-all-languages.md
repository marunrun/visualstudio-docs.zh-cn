---
title: 选项、文本编辑器、所有语言
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.JavaScript.General
- VS.ToolsOptionsPages.Text_Editor.ResJSON.General
- VS.ToolsOptionsPages.Text_Editor.All_Languages.General
- VS.ToolsOptionsPages.Text_Editor.Basic.General
- VS.ToolsOptionsPages.Text_Editor.CSharp.General
- VS.ToolsOptionsPages.Text_Editor.C/C++.General
- VS.ToolsOptionsPages.Text_Editor.CoffeeScript.General
- VS.ToolsOptionsPages.Text_Editor.CSS.General
- VS.ToolsOptionsPages.Text_Editor.Dockerfile.General
- VS.ToolsOptionsPages.Text_Editor.F#.General
- VS.ToolsOptionsPages.Text_Editor.Fsharp.General
- VS.ToolsOptionsPages.Text_Editor.HQL.General
- VS.ToolsOptionsPages.Text_Editor.HTML.General
- VS.ToolsOptionsPages.Text_Editor.HTML_(Web_Forms).General
- VS.ToolsOptionsPages.Text_Editor.JavaScript.General
- VS.ToolsOptionsPages.Text_Editor.TypeScript.General
- VS.ToolsOptionsPages.Text_Editor.JSON.General
- VS.ToolsOptionsPages.Text_Editor.LESS.General
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.General
- VS.ToolsOptionsPages.Text_Editor.SCSS.General
- VS.TOOLSOPTIONSPAGES.TEXT_EDITOR.SQL_SERVER_TOOLS.GENERAL
- VS.ToolsOptionsPages.Text_Editor.StreamAnalytics.General
- VS.ToolsOptionsPages.Text_Editor.T-SQL90.General
- VS.ToolsOptionsPages.Text_Editor.U-SQL.General
- VS.ToolsOptionsPages.Text_Editor.XAML.General
- VS.ToolsOptionsPages.Text_Editor.XML.General
helpviewer_keywords:
- Text Editor Options dialog box
- statement completion
- word wrap
- General dialog box
- line numbers
- virtual space
ms.assetid: 49ee7306-9d46-4170-850f-a1716171752d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9815bdec94ce32a3bfcc170dd95d834bc43ea58f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75566873"
---
# <a name="options-dialog-box-text-editor--all-languages"></a>“选项”对话框：“文本编辑器”\>“所有语言”

使用此对话框可更改代码编辑器的默认行为。 这些设置也适用于其他基于代码编辑器的编辑器，如 HTML 设计器的“源”视图。 若要打开此对话框，请从“工具”菜单中选择“选项”   。 在“文本编辑器”文件夹中，展开“所有语言”子文件夹，然后选择“常规”    。

> [!CAUTION]
> 在此页面用于设置所有开发语言的默认选项。 请记住，重置此对话框中的一个选项会将所有语言的“常规”选项重置为在此处选择的任何选项。 若要只为一种语言更改文本编辑器选项，请展开该语言的子文件夹并选择其选项页。

当在“常规”选项页上为某些编程语言选择了一个选项，而没有为其他编程语言选择该选项时，会显示一个灰色复选标记。

## <a name="statement-completion"></a>语句结束

**自动列出成员**

选中后，在编辑器中键入时，IntelliSense 会显示可用的成员、属性、值或方法的弹出列表。 从弹出列表中选择任何项即可将该项插入代码中。 选择此选项将启用“隐藏高级成员”选项  。

**隐藏高级成员**

选中后，通过只显示最常用的项，缩短弹出语句完成列表。 其他项从列表中被筛选掉。

**参数信息**

选中后，当前声明或过程的完整语法及其所有可用的参数显示在编辑器中的插入点下。 下一个可赋值参数以粗体显示。

## <a name="settings"></a>设置

**启用虚拟空格**

选中此选项并清除“自动换行”时，可以在代码编辑器中行尾以外的任意位置单击并键入  。 此功能可以用于将注释放置在代码旁的一致点处。

**自动换行**

选中后，行中水平方向超出可视编辑器区域的任何部分会自动显示在下一行。 选择此选项将启用“显示可视的自动换行标志符号”选项  。

> [!NOTE]
> “自动换行”打开时，“虚空格”功能会被关闭   。

**显示可视的自动换行标志符号**

选中后，在一个长行换行到第二行的位置会显示一个回车箭头指示符。

![LineBreakSymbol 屏幕快照](../../ide/reference/media/linebreak.gif)

如果不希望显示这些指示符，则清除此选项。

> [!NOTE]
> 这些提醒箭头不会添加到代码中，也不会打印出来。 它们仅供参考。

**行号**

选中后，行号出现在每行代码的旁边。

> [!NOTE]
> 这些行号不会添加到代码中，也不会打印出来。 它们仅供参考。

**启用单击 URL 定位**

选中后，鼠标光标在经过编辑器中的 URL 时会变成向上指的手形。 可以单击该 URL 以在 Web 浏览器中显示指示页面。

**导航栏**

选中后，将在代码编辑器的顶部显示“导航栏”  。 它的下拉“对象”和“成员”列表可用于在代码中选择特定的对象，从它的成员中选择，然后导航到代码编辑器中选定成员的声明   。

**没有选定内容时对空行应用剪切或复制命令**

此选项设置当你将插入点放置在空行上，未选中任何内容，然后复制或剪切时，编辑器的行为。

- 选中此选项后，将复制或剪切空行。 如果随后执行粘贴操作，会插入一个新的空行。

- 清除此选项后，“剪切”命令将移除空行。 但仍保留剪贴板中的数据。 因此，如果随后使用“粘贴”命令，则会粘贴最近复制到剪贴板的内容。 如果先前没有复制任何内容，则不会粘贴任何内容。

此设置对行非空时的复制或剪切操作无效。 如果未选择任何内容，将会对整行进行复制或剪切。 如果随后执行粘贴操作，则粘贴整行文本及其行尾字符。

> [!TIP]
> 若要显示空格、制表符和行尾的指示符，从而区分缩进行和完全空白的行，请从“编辑”菜单中选择“高级”，然后选择“查看空白”    。

## <a name="see-also"></a>请参阅

- [“选项”->“文本编辑器”->“所有语言”->“选项卡”](../../ide/reference/options-text-editor-all-languages-tabs.md)
- [“选项”对话框 ->“环境”->“常规”](../../ide/reference/general-environment-options-dialog-box.md)
- [使用 IntelliSense](../../ide/using-intellisense.md)
