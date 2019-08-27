---
title: 代码度量值窗口
ms.date: 12/12/2017
ms.topic: reference
f1_keywords:
- vs.codemetrics.output
helpviewer_keywords:
- code metrics results
- code metrics results window
- results window, code metrics
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bbe2c216a9293ddc8c5c1212957c2987924d14e1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62825066"
---
# <a name="use-the-code-metrics-results-window"></a>使用代码度量结果窗口

**代码度量结果**窗口将显示生成的代码度量值分析的数据。 代码度量数据值的详细信息，请参阅[代码的指标值](../code-quality/code-metrics-values.md)。

## <a name="display-code-metrics-results"></a>显示代码度量结果

**代码度量结果**生成代码度量结果时，将自动显示窗口。 此外可以在任何时候显示窗口。

可以显示代码度量结果窗口使用以下菜单序列中的一个：

- 上**分析**菜单中，选择**Windows** > **代码度量结果**。

- 上**视图**菜单中，选择**其他 Windows** > **代码度量结果**。

**代码度量结果**窗口将打开，即使不包含任何结果。

### <a name="to-view-code-metrics-details"></a>若要查看代码度量值详细信息

如果已生成代码度量结果，则展开的树中**层次结构**列。

## <a name="filter-code-metrics-results"></a>筛选代码度量结果

您可以筛选结果中显示**代码度量结果**窗口是通过使用顶部的工具栏。 例如，您可能想要查看具有低于 65 可维护性索引的结果。

**筛选器**下拉列表框中包含的结果列的名称。 定义筛选器时，则将它添加到并进行缩进列表的底部。 该列表可以包含未定义的最后 10 个筛选器。

### <a name="to-filter-the-code-metrics-results"></a>若要筛选代码度量结果

1. 从**筛选器**列表中，选择的列名称。

2. 在中**Min**，键入要显示的最小值。

3. 在中**最大**，键入要显示的最大值。

4. 单击**应用筛选器**按钮。

5. 若要查看结果详细信息，请展开层次结构树。

## <a name="add-remove-and-rearrange-data-columns"></a>添加、 删除和重新排列的数据列

您可以添加或删除的结果中的列**代码度量结果**窗口。 此外，以使它们显示在所需的顺序可以重新排列结果列。

### <a name="add-or-remove-a-column"></a>添加或删除列

1. 单击**添加/删除列**按钮，或右键单击任何列标题，然后单击**添加/删除列**。

1. 在中**添加/删除列**对话框中，选中或清除的复选框以添加或删除，然后选择所需的列**确定**。

### <a name="rearrange-columns"></a>重新排列列

1. 单击**添加/删除列**按钮。

1. 在中**添加/删除列**对话框框中，选择你想要移动，然后选择向上箭头或向下箭头的列。

1. 当列位于所需的位置时，选择**确定**。

## <a name="copy-data-to-the-clipboard-or-excel"></a>将数据复制到剪贴板或 Excel

可以选择并复制到剪贴板作为文本字符串都包含一行的名称和每个数据列的值为所选的行的代码度量数据。 此外可以单击**在 Microsoft Excel 中打开所选内容**将所有代码度量结果导出到 Excel 电子表格。

## <a name="create-a-work-item-based-on-code-metric-results"></a>创建工作项根据代码度量结果

您可以创建[Azure 板](/azure/devops/boards/index?view=vsts)基于工作项会导致**代码度量结果**窗口。 当创建工作项时，Visual Studio 会自动输入中的标题**标题**下的字段和代码度量值数据**历史记录**选项卡。

详细了解 Azure 板的工作项，请参阅[的工作项](/azure/devops/boards/work-items/index?view=vsts)。

### <a name="to-create-a-work-item-based-on-a-result"></a>若要创建基于某一结果的工作项

1. 右键单击结果。

2. 指向**创建工作项**，然后单击你想要创建的工作项类型 (**Bug**，**任务**，依此类推)。

3. 通过填写所有必填字段来完成工作项窗体。

4. 上**文件**菜单上，单击**全部保存**来保存工作项。

### <a name="to-create-a-bug-based-on-a-result"></a>若要创建基于某一结果的 bug

1. 单击以选中它的结果。

2. 单击**创建工作项**按钮。

3. 通过填写所有必填字段来完成工作项窗体。

4. 上**文件**菜单上，单击**全部保存**来保存工作项。

## <a name="see-also"></a>请参阅

- [代码度量值](../code-quality/code-metrics-values.md)
- [如何：生成代码度量数据](../code-quality/how-to-generate-code-metrics-data.md)