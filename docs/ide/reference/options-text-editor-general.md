---
title: 选项，文本编辑器，常规
ms.date: 01/18/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor
- vs.toolsoptionspages.text_editor
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting
- VS.ToolsOptionsPages.Text_Editor.CSharp.Outlining
- VS.ToolsOptionsPages.Text_Editor.General
- VS.ToolsOptionsPages.Text_Editor.PL/SQL
- VS.ToolsOptionsPages.Text_Editor.PL/SQL.General
- VS.ToolsOptionsPages.Text_Editor.Python
- VS.ToolsOptionsPages.Text_Editor.R
- VS.ToolsOptionsPages.Text_Editor.RDL_Expression.General
- VS.ToolsOptionsPages.Text_Editor.SQL
- VS.ToolsOptionsPages.Text_Editor.SQL.General
- VS.ToolsOptionsPages.Text_Editor.SQL_Script
- VS.ToolsOptionsPages.Text_Editor.SQL_Script.General
- VS.ToolsOptionsPages.Text_Editor.T-SQL
- VS.ToolsOptionsPages.Text_Editor.T-SQL.General
- VS.ToolsOptionsPages.Text_Editor.T-SQL7.General
- VS.ToolsOptionsPages.Text_Editor.T-SQL80
- VS.ToolsOptionsPages.Text_Editor.T-SQL80.General
helpviewer_keywords:
- Text Editor Options dialog box
- Code Editor
- Text Editor [Visual Studio]
- editors, global settings
ms.assetid: 4ac21e48-3243-4141-9058-7eaf12b3cde7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ebe526bbac859777edb4c2c78c65a1cdbd27fc85
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75568407"
---
# <a name="options-dialog-box-text-editor--general"></a>“选项”对话框：“文本编辑器”\>“常规”

使用此对话框可以更改 Visual Studio 代码和文本编辑器的全局设置。 若要显示此对话框，请在“工具”菜单上选择“选项”，展开“文本编辑器”文件夹，然后选择“常规”     。

## <a name="settings"></a>设置

### <a name="drag-and-drop-text-editing"></a>拖放文本编辑

勾选此项后，使用鼠标选定文本并将其拖到当前文档的其他位置或任何其他打开的文档中，即可移动文本。

### <a name="automatic-delimiter-highlighting"></a>自动突出显示分隔符

勾选此项后，将突出显示分隔参数、项值对以及成对大括号的分隔符字符。

### <a name="track-changes"></a>跟踪更改

选定代码编辑器后，所选内容的边距中会出现一条垂直的黄线，标记自文件上次保存后更改的代码。 保存更改时，竖线变为绿色。

### <a name="auto-detect-utf-8-encoding-without-signature"></a>自动检测不带签名的 UTF-8 编码

默认情况下，编辑器通过搜索字节顺序标记或字符集标记检测编码。 如果在当前文档中两者均未找到，代码编辑器会尝试通过扫描字节序列来自动检测 UTF-8 编码。 若要禁用自动检测编码，请清除此选项。

### <a name="follow-project-coding-conventions"></a>遵循项目编码约定

如果你选中此选项，项目的指定编码约定就会替代你对个人项目使用的任何编码约定。

### <a name="enable-mouse-click-to-perform-go-to-definition"></a>启用通过鼠标单击执行“转到定义”

如果选中此选项，可以在单击鼠标的同时，按 Ctrl  并将鼠标悬停在元素之上。 这样，就可以转到选定元素的定义了。 也可以从“使用修改键”  下拉列表中选择“Alt”  或“Ctrl   + Alt  ”。

选中“在速览视图中打开定义”  复选框，可以在窗口中显示元素定义，而无需离开代码编辑器中的当前位置。

## <a name="display"></a>显示

### <a name="selection-margin"></a>选定内容的边距

勾选此项后，将显示编辑器文本区域的左侧边缘的垂直边距。 可以通过单击此边距选择一整行文本，或者通过单击并拖动，选择连续多行文本。

|打开选定内容的边距|关闭选定内容的边距|
| - | - |
|![HTMLpageSelectionMarginOn 屏幕快照](../../ide/reference/media/vxselmaron.gif)|![HTMLpageSelectionMarginOff 屏幕快照](../../ide/reference/media/vxselmaroff.gif)|

### <a name="indicator-margin"></a>指示器边距

勾选此项后，将显示编辑器文本区域的左侧边缘外的垂直边距。 在此边距内单击时，会显示与文本有关的图标和工具提示。 例如，指示器边距内会出现断点或任务列表快捷方式。 指示器边距信息不会打印输出。

### <a name="highlight-current-line"></a>突出显示当前行

勾选此项后，光标所在代码行周围会显示一个灰色框。

### <a name="show-structure-guide-lines"></a>显示结构参考线

如果你选中此选项，与结构化代码块对齐的竖线就会在编辑器中显示，这样你就能轻松识别各个代码块了。

## <a name="see-also"></a>请参阅

- [“选项”->“文本编辑器”->“所有语言”](../../ide/reference/options-text-editor-all-languages.md)
- [“选项”->“文本编辑器”->“所有语言”->“选项卡”](../../ide/reference/options-text-editor-all-languages-tabs.md)
- [“选项”->“文本编辑器”->“文件扩展名”](../../ide/reference/options-text-editor-file-extension.md)
- [标识并自定义键盘快捷键](../../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)
- [自定义编辑器](../how-to-change-text-case-in-the-editor.md)
- [使用 IntelliSense](../../ide/using-intellisense.md)
