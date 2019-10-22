---
title: “选项”->“文本编辑器”->“常规”| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.TOOLSOPTIONSPAGES.TEXT_EDITOR.SQL_SERVER_TOOLS.GENERAL
- VS.ToolsOptionsPages.Text_Editor.All_Languages.General
- VS.ToolsOptionsPages.Text_Editor.RDL_Expression.General
- VS.ToolsOptionsPages.Text_Editor.SQL.General
- vs.toolsoptionspages.text_editor
- VS.ToolsOptionsPages.Text_Editor.XML.General
- VS.ToolsOptionsPages.Text_Editor.T-SQL80.General
- VS.ToolsOptionsPages.Text_Editor.CSS
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.General
- VS.ToolsOptionsPages.Text_Editor.Visual_JSharp.General
- VS.ToolsOptionsPages.Text_Editor.SQL_Script.General
- VS.ToolsOptionsPages.Text_Editor.CSharp.General
- VS.ToolsOptionsPages.Text_Editor.All_Languages
- VS.ToolsOptionsPages.Text_Editor.T-SQL7.General
- VS.ToolsOptionsPages.Text_Editor.Basic.General
- VS.ToolsOptionsPages.Text_Editor.T-SQL.General
- vs.toolsoptionspages.text_editor.visual_jsharp
- VS.ToolsOptionsPages.Text_Editor.F#.Tabs
- VS.ToolsOptionsPages.Text_Editor.F#
- VS.ToolsOptionsPages.Text_Editor.PL/SQL.General
- VS.ToolsOptionsPages.Text_Editor.C/C++.General
- VS.ToolsOptionsPages.Text_Editor.Plain_Text
- VS.ToolsOptionsPages.Text_Editor.HTML
- VS.ToolsOptionsPages.Text_Editor.XAML.General
- VS.ToolsOptionsPages.Text_Editor
- VS.ToolsOptionsPages.Text_Editor.F#.General
- VS.ToolsOptionsPages.Text_Editor.XOML.General
- VS.ToolsOptionsPages.Text_Editor.SQL
- vs.toolsoptionspages.text_editor.c/c++
- VS.ToolsOptionsPages.Text_Editor.SQL_Script
- VS.ToolsOptionsPages.Text_Editor.T-SQL90.General
- VS.ToolsOptionsPages.Text_Editor.General
- VS.ToolsOptionsPages.Text_Editor.CSharp
helpviewer_keywords:
- Text Editor Options dialog box
- Code Editor
- Text Editor [Visual Studio]
- editors, global settings
ms.assetid: 4ac21e48-3243-4141-9058-7eaf12b3cde7
caps.latest.revision: 34
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fa81b08d6e375da4ad67b2e6eec32f244a779408
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662253"
---
# <a name="options-text-editor-general"></a>选项，文本编辑器，常规
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用此对话框可以更改 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 代码和文本编辑器的全局设置。 若要显示此对话框，请在“工具”菜单上单击“选项”，展开“文本编辑器”文件夹，然后单击“常规”。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。

## <a name="settings"></a>设置
 选择后，拖放文本编辑功能，您可以通过选择文本并将其拖放到当前文档或任何其他打开的文档中的其他位置来移动文本。

 自动分隔符突出显示选中后，分隔参数或项值对以及匹配大括号的分隔符将突出显示。

 跟踪所做的更改。选择代码编辑器后，选择边距中会出现一条黄色竖线，用于标记自上次保存文件以来发生更改的代码。 保存更改时，竖线变为绿色。

 自动检测不带签名的 UTF-8 编码默认情况下，编辑器通过搜索字节顺序标记或字符集标记来检测编码。 如果在当前文档中两者均未找到，代码编辑器将尝试通过扫描字节序列，自动检测 UTF-8 编码。 若要禁用自动检测编码，请清除此选项。

## <a name="display"></a>显示
 选择边距选择后，沿编辑器文本区域的左边缘显示垂直边距。 可以通过单击此边距选择一整行文本，或者通过单击并拖动，选择连续多行文本。

|打开选定内容的边距|关闭选定内容的边距|
|-------------------------|--------------------------|
|![HTMLpageSelectionMarginOn 屏幕快照](../../ide/reference/media/vxselmaron.gif "|::ref1::|")|![HTMLpageSelectionMarginOff 屏幕快照](../../ide/reference/media/vxselmaroff.gif "|::ref2::|")|

 指示器边距选中后，将在编辑器文本区域的左边缘之外显示垂直边距。 在此边距内单击时，会显示与文本有关的图标和工具提示。 例如，指示器边距内会出现断点或任务列表快捷方式。 但不显示指示器边距信息。

 选中时垂直滚动条，将显示一个垂直滚动条，使您可以向上或向下滚动以查看在编辑器查看区域外的元素。 如果垂直滚动条不可用，可以使用 Page Up、Page Down 键和光标键滚动。

 水平滚动条（如果选中）将显示水平滚动条，它允许您从两侧滚动以查看编辑器查看区域外的元素。 如果水平滚动条不可用，可以使用光标键滚动。

 选中时突出显示当前行，在光标所在的代码行周围显示灰色框。

## <a name="see-also"></a>另请参阅
 [选项，文本编辑器，所有语言](../../ide/reference/options-text-editor-all-languages.md)[选项，文本编辑器，所有语言，选项卡](../../ide/reference/options-text-editor-all-languages-tabs.md)[选项，文本编辑器，文件扩展名](../../ide/reference/options-text-editor-file-extension.md) [标识和自定义使用的键盘快捷方式](../../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md) [Customizing 编辑器](../../ide/customizing-the-editor.md) [Using IntelliSense](../../ide/using-intellisense.md)
