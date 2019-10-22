---
title: “选项”->“文本编辑器”->“所有语言”| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.JavaScript.General
- VS.ToolsOptionsPages.Text_Editor.ResJSON.General
- vs.toolsoptionspages.text_editor.all_languages.scrollbars
helpviewer_keywords:
- Text Editor Options dialog box
- statement completion
- word wrap
- General dialog box
- line numbers
- virtual space
ms.assetid: 49ee7306-9d46-4170-850f-a1716171752d
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ebe2da1dec9917a792f3e4e02516a79cff605c80
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662401"
---
# <a name="options-text-editor-all-languages"></a>选项、文本编辑器、所有语言
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用此对话框可更改代码编辑器的默认行为。 这些设置也适用于其他基于代码编辑器的编辑器，如 HTML 设计器的“源”视图。 若要打开此对话框，请从“工具”菜单中选择“选项”   。 在“文本编辑器”文件夹中，展开“所有语言”子文件夹，然后选择“常规”    。

> [!CAUTION]
> 在此页面用于设置所有开发语言的默认选项。 请记住，重置此对话框中的一个选项会将所有语言的“常规”选项重置为在此处选择的任何选项。 若要只为一种语言更改文本编辑器选项，请展开该语言的子文件夹并选择其选项页。

 当在“常规”选项页上为某些编程语言选择了一个选项，而没有为其他编程语言选择该选项时，会显示一个灰色复选标记。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。

## <a name="statement-completion"></a>语句结束
 自动列出成员选定后，在编辑器中键入时，可通过 IntelliSense 显示可用成员、属性、值或方法的弹出列表。 从弹出列表中选择任何项即可将该项插入代码中。 选择此选项将启用“隐藏高级成员”选项  。

 选中时隐藏高级成员，通过仅显示最常用的项来缩短弹出语句完成列表。 其他项从列表中被筛选掉。

 参数信息选定后，当前声明或过程的完整语法会显示在编辑器中的插入点下，并显示其所有可用参数。 下一个可赋值参数以粗体显示。

## <a name="settings"></a>设置
 启用虚拟空间选择此选项并清除 "**自动换**行" 时，可以单击代码编辑器中行末尾以外的任意位置，然后键入。 此功能可以用于将注释放置在代码旁的一致点处。

 选中时自动换行，在 "可视编辑器" 区域中水平扩展的行的任何部分都将自动显示在下一行。 选择此选项将启用“显示可视的自动换行标志符号”选项  。

> [!NOTE]
> “自动换行”打开时，“虚空格”功能会被关闭   。

 显示可视的自动换行标志符号选中时，会在长行换行的位置显示返回箭头指示符。

 ![LineBreakSymbol 屏幕快照](../../ide/reference/media/linebreak.gif "linebreak")

 如果不希望显示这些指示符，则清除此选项。

> [!NOTE]
> 这些提醒箭头不会添加到代码中，也不会打印出来。 它们仅供参考。

 在没有选定内容时对空行应用剪切或复制命令此选项在您将插入点放置在空行上时设置编辑器的行为，不选择任何内容，然后复制或剪切。

- 选中此选项后，将复制或剪切空行。 如果随后执行粘贴操作，会插入一个新的空行。

- 清除此选项后，“剪切”命令将移除空行。 但仍保留剪贴板中的数据。 因此，如果随后使用“粘贴”命令，则会粘贴最近复制到剪贴板的内容。 如果先前没有复制任何内容，则不会粘贴任何内容。

  此设置对行非空时的复制或剪切操作无效。 如果未选择任何内容，将会对整行进行复制或剪切。 如果随后执行粘贴操作，则粘贴整行文本及其行尾字符。

> [!TIP]
> 若要显示空格、制表符和行尾的指示符，从而区分缩进行和完全空白的行，请从“编辑”菜单中选择“高级”，然后选择“查看空白”    。

## <a name="display"></a>显示
 行号选择后，每个代码行旁边都会出现一个行号。

> [!NOTE]
> 这些行号不会添加到代码中，也不会打印出来。 它们仅供参考。

 启用单击 URL 导航选中此项后，鼠标光标将在编辑器中传递 URL 时变为手形。 可以单击该 URL 以在 Web 浏览器中显示指示页面。

 导航栏在选中后会在代码编辑器的顶部显示**导航栏**。 它的下拉“对象”和“成员”列表可用于在代码中选择特定的对象，从它的成员中选择，然后导航到代码编辑器中选定成员的声明   。

## <a name="see-also"></a>另请参阅
 "[选项"、"文本编辑器"、"所有语言"、](../../ide/reference/options-text-editor-all-languages-tabs.md) "[常规"、"环境和选项" 对话框](../../ide/reference/general-environment-options-dialog-box.md)[使用 IntelliSense](../../ide/using-intellisense.md)
