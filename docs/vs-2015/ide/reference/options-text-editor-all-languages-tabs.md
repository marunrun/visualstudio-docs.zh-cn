---
title: “选项”->“文本编辑器”->“所有语言”->“制表符”| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.ResJSON.Tabs
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Tabs
- VS.ToolsOptionsPages.Text_Editor.All_Languages.Tabs
helpviewer_keywords:
- indents, Code Editor
- Code Editor, default behavior
- tabs, setting in Code Editor
- All Languages Text Editor Options dialog box
- editors, Code Editor
- Code Editor, indenting
- Code Editor, tabs
ms.assetid: 7e208e1d-5e3a-4bf7-a27b-4417e3e049c7
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4cb670ab52e321f15c5b009c66ca40623409f10a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662388"
---
# <a name="options-text-editor-all-languages-tabs"></a>选项，文本编辑器，所有语言，选项卡
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用此对话框可更改代码编辑器的默认行为。 这些设置也适用于其他基于代码编辑器的编辑器，如 HTML 设计器的“源”视图。 若要显示这些选项，请选择“工具”菜单中的“选项”   。 在“文本编辑器”中，展开“所有语言”子文件夹，然后选择“制表符”    。

> [!CAUTION]
> 在此页面用于设置所有开发语言的默认选项。 请记住，重置此对话框中的一个选项会将所有语言的“制表符”选项重置为在此处选择的任何选项。 若要只为一种语言更改文本编辑器选项，请展开该语言的子文件夹并选择其选项页。

 如果在“制表符”选项页上为特定的编程语言选择了不同的设置，则对于不同的“缩进”选项，将显示消息“各种文本格式的缩进设置相互冲突”；对于不同的“制表符”选项，将显示消息“各种文本格式的制表符设置相互冲突”   。 例如，如果为 Visual Basic 选择了“智能缩进”选项，但为 Visual C++ 选择了“块缩进”，则会显示此提醒   。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。

## <a name="indenting"></a>缩进
 不选择时无缩进新行。 插入点被置于新行的第一列。

 阻止选择此选项后，新行将自动缩进。 插入点被置于与上一行相同的起始点处。

 选中后，新行的放置依据开发语言的其他代码格式设置和 IntelliSense 约定，以适应代码上下文。 此选项并不是对所有开发语言都可用。

 例如，括在左括号 ({) 和右括号 (}) 之间的行可能从对齐括号的位置自动缩进一个额外的制表位。

## <a name="tabs"></a>制表符
 选项卡大小设置制表位之间的距离（以空格为间隔）。 默认值为 4 个空格。

 缩进大小设置自动缩进的大小（以空格为间隔）。 默认值为 4 个空格。 将插入制表符和/或空格字符来填充指定的大小。

 插入空格如果选中，缩进操作只插入空格字符，而不插入制表符。 例如，如果“缩进大小”设置为 5，则每当按 Tab 键或单击“格式设置”工具栏上的“增加缩进”按钮时，都会插入五个空格字符    。

 保留选项卡选择后，缩进操作会插入尽可能多的制表符。 每个制表符都会填充“制表符大小”中指定的空格数  。 如果“缩进大小”不是“制表符大小”的偶数倍，则会添加空格字符以填充差额   。

## <a name="see-also"></a>另请参阅
 [选项，文本编辑器，所有语言](../../ide/reference/options-text-editor-all-languages.md)[常规，环境，选项对话框](../../ide/reference/general-environment-options-dialog-box.md)
