---
title: "\"代码度量\" 窗口"
ms.date: 12/12/2017
ms.topic: reference
f1_keywords:
- vs.codemetrics.output
helpviewer_keywords:
- code metrics results
- code metrics results window
- results window, code metrics
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0824fe608ad1bac86ef904702bd1be907bc9ce7d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648998"
---
# <a name="use-the-code-metrics-results-window"></a>使用 "代码度量结果" 窗口

"**代码度量结果**" 窗口显示由代码度量值分析生成的数据。 有关代码度量值数据值的详细信息，请参阅[代码度量值](../code-quality/code-metrics-values.md)。

## <a name="display-code-metrics-results"></a>显示代码度量结果

生成代码度量值结果时，将自动显示 "**代码度量结果**" 窗口。 你还可以随时显示窗口。

您可以使用以下菜单序列之一显示 "代码度量结果" 窗口：

- 在 "**分析**" 菜单上，选择 " **Windows**  > **代码度量结果**"。

- 在 "**视图**" 菜单上，选择 "**其他 Windows**  > **代码度量值结果**"。

"**代码度量值" 结果**窗口将打开，即使它不包含任何结果。

### <a name="to-view-code-metrics-details"></a>查看代码度量详细信息

如果已生成代码度量结果，则在 "**层次结构**" 列中展开树。

## <a name="filter-code-metrics-results"></a>筛选代码度量结果

您可以使用顶部的工具栏筛选 "**代码度量结果**" 窗口中显示的结果。 例如，你可能只想查看在65以下具有可维护性索引的结果。

"**筛选器**" 下拉框中包含结果列的名称。 定义筛选器后，会将其添加到列表的底部，同时添加缩进。 列表可以包含定义的最后10个筛选器。

### <a name="to-filter-the-code-metrics-results"></a>筛选代码度量结果

1. 从 "**筛选器**" 列表中，选择列名称。

2. 在 "**最**小值" 中，键入要显示的最小值。

3. 在 "**最**大值" 中，键入要显示的最大值。

4. 单击 "**应用筛选器**" 按钮。

5. 若要查看结果详细信息，请展开层次结构树。

## <a name="add-remove-and-rearrange-data-columns"></a>添加、删除和重新排列数据列

您可以从 "**代码度量值结果**" 窗口中添加或删除结果列。 此外，您可以重新排列结果列，使其按您需要的顺序显示。

### <a name="add-or-remove-a-column"></a>添加或删除列

1. 单击 "**添加/删除列**" 按钮，或右键单击任意列标题，然后单击 "**添加/删除列**"。

1. 在 "**添加/删除列**" 对话框中，选中或清除要添加或删除的列的复选框，然后选择 **"确定"** 。

### <a name="rearrange-columns"></a>重新排列列

1. 单击 "**添加/删除列**" 按钮。

1. 在 "**添加/删除列**" 对话框中，选择要移动的列，然后选择向上箭头或向下箭头。

1. 将列定位到所需位置后，选择 **"确定"** 。

## <a name="copy-data-to-the-clipboard-or-excel"></a>将数据复制到剪贴板或 Excel

对于每个数据列的名称和值，你可以选择并将所选的代码度量数据行复制到剪贴板，作为文本字符串。 还可以单击 "**在 Microsoft excel 中打开所选内容**" 将所有代码度量结果导出到 Excel 电子表格。

## <a name="create-a-work-item-based-on-code-metric-results"></a>基于代码度量结果创建工作项

你可以创建基于 "**代码度量结果**" 窗口中的结果的[Azure Boards](/azure/devops/boards/index?view=vsts)工作项。 创建工作项后，Visual Studio 会自动在 "**历史记录**" 选项卡下的 "**标题**" 字段和代码度量数据中输入一个标题。

有关 Azure Boards 工作项的详细信息，请参阅[工作项](/azure/devops/boards/work-items/index?view=vsts)。

### <a name="to-create-a-work-item-based-on-a-result"></a>基于结果创建工作项

1. 右键单击结果。

2. 指向 "**创建工作项**"，然后单击要创建的工作项类型（**Bug**、**任务**，等等）。

3. 填写所有必填字段，完成工作项窗体。

4. 在 "**文件**" 菜单上，单击 "**全部保存**" 以保存工作项。

### <a name="to-create-a-bug-based-on-a-result"></a>基于结果创建 bug

1. 单击结果将其选中。

2. 单击 "**创建工作项**" 按钮。

3. 填写所有必填字段，完成工作项窗体。

4. 在 "**文件**" 菜单上，单击 "**全部保存**" 以保存工作项。

## <a name="see-also"></a>请参阅

- [代码度量值](../code-quality/code-metrics-values.md)
- [如何：生成代码度量数据](../code-quality/how-to-generate-code-metrics-data.md)
