---
title: U-SQL 编辑器格式化选项
ms.date: 01/17/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.U-SQL.Formatting.Spacing
- VS.ToolsOptionsPages.Text_Editor.U-SQL.Formatting.NewLines
- VS.ToolsOptionsPages.Text_Editor.U-SQL.Formatting.Indentation
- VS.ToolsOptionsPages.Text_Editor.U-SQL.Formatting
- VS.ToolsOptionsPages.Text_Editor.U-SQL.Formatting.General
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d1e57470c1afa0fad97265bdcebff4fd9a2a0a43
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72666669"
---
# <a name="options-text-editor-u-sql-formatting"></a>“选项”>“文本编辑器”>“U-SQL”>“格式化”

通过“格式设置”选项页面，可在代码编辑器中设定代码格式设置选项  。 要访问此选项页，请选择“工具” > 选项”   。 在“选项”  对话框中，依次选择“文本编辑器”   > “U-SQL”   > “格式化”  。

## <a name="general-page"></a>常规页

### <a name="general-settings"></a>常规设置

这些设置将影响代码编辑器向代码应用格式设置选项的时间  。

- **输入分号后自动格式化已完成语句**

   如果你选中此项，编辑器就会在你选择分号键时根据你为编辑器选择的格式化选项来格式化语句。

- 粘贴时自动设置格式 

   如果选中此项，设置粘贴到编辑器中的文本的格式，使其与为编辑器选择的格式设置选项一致。

## <a name="preview-windows"></a>预览窗口

“缩进”  、“新行”  和“间距”  子页都在底部显示预览窗口。 预览窗口显示每个选项的效果。 若要使用预览窗口，请选择一个格式设置选项。 预览窗口显示选定选项的示例。 如果你通过选中复选框来更改设置，预览窗口就会更新为显示新设置的效果。

### <a name="indentation-remarks"></a>缩进备注

每种语言下，“选项卡”页的缩进选项仅确定你在行尾按 Enter 时，代码编辑器将光标置于何处   。 如果代码自动格式化，“格式化”  下的缩进选项就会应用，例如：

- 在选中“在粘贴后自动格式化”  的情况下将代码粘贴到文件中时
- 当手动键入要格式化的代码块时

## <a name="see-also"></a>请参阅

- [“选项”对话框 ->“环境”->“常规”](../../ide/reference/general-environment-options-dialog-box.md)