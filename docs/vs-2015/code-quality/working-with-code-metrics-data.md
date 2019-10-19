---
title: 使用代码度量数据 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codemetrics.output
helpviewer_keywords:
- code metrics results
- code metrics results window
- results window, code metrics
ms.assetid: 988193ec-b4a3-4e11-b5a1-7334979807d5
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3c2460b4e8b9e0b9043178989fcf8825815471be
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645710"
---
# <a name="working-with-code-metrics-data"></a>使用代码度量数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

"**代码度量结果**" 窗口显示由代码度量值分析生成的数据。 有关代码度量值数据值的详细信息，请参阅[代码度量值](../code-quality/code-metrics-values.md)。

 本主题包含以下各节：

- [Code Metrics Results Window](../code-quality/working-with-code-metrics-data.md#BKMK_CodeMetricsResultsWindow)

- [显示代码度量结果](../code-quality/working-with-code-metrics-data.md#BKMK_DisplayingCodeMetricsResults)

- [筛选代码度量结果](../code-quality/working-with-code-metrics-data.md#BKMK_FilteringCodeMetricsResults)

- [添加、删除和重新排列数据列](../code-quality/working-with-code-metrics-data.md#BKMK_AddingRemovingandRearrangingDataColumns)

- [将数据复制到剪贴板或 Excel](../code-quality/working-with-code-metrics-data.md#BKMK_Copying_Data_to_the_Clipboard_or_Excel)

- [基于代码度量结果创建工作项](../code-quality/working-with-code-metrics-data.md#BKMK_Creating_a_Work_Item_Based_on_Code_Metric_Results)

## <a name="BKMK_CodeMetricsResultsWindow"></a> Code Metrics Results Window
 "**代码度量结果**" 窗口顶部有一个工具栏，并显示计算结果的列。

|列|描述|
|------------|-----------------|
|**层次结构**|"**层次结构**" 列包含代码层次结构的树视图，您可以展开或折叠它以查看所需的详细信息级别。 其余列显示计算结果。 您可以根据需要隐藏或排列结果列。|
|**易**|可**维护性**列包含一个图标以及数值结果。 绿色图标表示可维护性相对较高。 黄色图标表示可维护性程度适中。 红色图标表示可维护性和潜在问题点。 这些颜色指示器对应于 FxCop 规则 AvoidUnmaintainableCode 使用的严重性类别。 如果可维护性索引低于10，则此规则会引发错误，如果索引介于10到20之间，则会发出警告; 如果索引大于20，则不会出现警告。 可维护性索引是三个指标的合成：圈复杂度、代码行和计算复杂性。 它的值不以单位表示。|

## <a name="BKMK_DisplayingCodeMetricsResults"></a>显示代码度量结果
 生成代码度量值结果时，将自动显示 "代码度量结果" 窗口。 你还可以随时显示窗口。

#### <a name="to-display-the-code-metrics-results-window"></a>显示 "代码度量结果" 窗口

- 在 "**分析**" 菜单上，单击 " **Windows** "，然后单击 "**代码度量值结果**"。

     \- 或 -

- 在 "**视图**" 菜单上，指向 "**其他窗口**"，再单击 "**代码度量值结果**"。

     即使不包含任何结果，也会显示 "代码度量结果" 窗口。

#### <a name="to-view-code-metrics-details"></a>查看代码度量详细信息

- 如果已生成代码度量结果，则在 "**层次结构**" 列中展开树。

## <a name="BKMK_FilteringCodeMetricsResults"></a>筛选代码度量结果
 您可以使用顶部的工具栏筛选 "**代码度量结果**" 窗口中显示的结果。 例如，你可能只想查看在65以下具有可维护性索引的结果。

 "**筛选器**" 下拉框中包含结果列的名称。 定义筛选器后，会将其添加到列表的底部，同时添加缩进。 列表可以包含定义的最后十个筛选器。

#### <a name="to-filter-the-code-metrics-results"></a>筛选代码度量结果

1. 从 "**筛选器**" 列表中，选择列名称。

2. 在 "**最**小值" 中，键入要显示的最小值。

3. 在 "**最**大值" 中，键入要显示的最大值。

4. 单击 "**应用筛选器**" 按钮。

5. 若要查看结果详细信息，请展开层次结构树。

## <a name="BKMK_AddingRemovingandRearrangingDataColumns"></a>添加、删除和重新排列数据列
 您可以从 "**代码度量值结果**" 窗口中添加或删除结果列。 此外，您可以重新排列结果列，使其按您需要的顺序显示。

#### <a name="to-remove-a-column"></a>删除列

1. 单击 "**添加/删除列**" 按钮。

     \- 或 -

     右键单击任何列标题，然后单击 "**添加/删除列**"。

2. 在 "**添加/删除列**" 对话框中，清除要删除的列的复选框，然后单击 **"确定"** 。

#### <a name="to-add-a-previously-removed-column"></a>添加以前删除的列

1. 单击 "**添加/删除列**" 按钮。

     \- 或 -

     右键单击任何列标题，然后单击 "**添加/删除列**"。

2. 在 "**添加/删除列**" 对话框中，选中要添加的列的复选框，然后单击 **"确定"** 。

#### <a name="to-rearrange-columns"></a>重新排列列

1. 单击 "**添加/删除列**" 按钮。

     \- 或 -

     右键单击任何列标题，然后单击 "**添加/删除列**"。

2. 在 "**添加/删除列**" 对话框中，选择要移动的列，然后单击向上箭头或向下箭头。

3. 将列定位到所需位置后，单击 **"确定"** 。

## <a name="BKMK_Copying_Data_to_the_Clipboard_or_Excel"></a>将数据复制到剪贴板或 Excel
 对于每个数据列的名称和值，你可以选择并将所选的代码度量数据行复制到剪贴板，作为文本字符串。 还可以单击 "**在 Microsoft excel 中打开列表**" 将所有代码度量结果导出到 Excel 电子表格

## <a name="BKMK_Creating_a_Work_Item_Based_on_Code_Metric_Results"></a>基于代码度量结果创建工作项
 你可以创建基于 "**代码度量结果**" 窗口中的结果的 [!INCLUDE[esprfound](../includes/esprfound-md.md)] 工作项。 创建工作项后，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 会自动在 "**历史记录**" 选项卡下的 "**标题**" 字段和代码度量数据中输入一个标题。

 有关如何创建工作项的详细信息，请参阅[创建重定向&#93;的&#91;工作项](https://msdn.microsoft.com/24b2e064-16ac-4bf0-8de4-98a1f48b8c4b)。

#### <a name="to-create-a-work-item-based-on-a-result"></a>基于结果创建工作项

1. 右键单击结果。

2. 指向 "**创建工作项**"，然后单击要创建的工作项类型（**Bug**、**任务**，等等）。

3. 填写所有必填字段，完成工作项窗体。

4. 在 "**文件**" 菜单上，单击 "**全部保存**" 以保存工作项。

#### <a name="to-create-a-bug-based-on-a-result"></a>基于结果创建 bug

1. 单击结果将其选中。

2. 单击 "**创建工作项**" 按钮。

3. 填写所有必填字段，完成工作项窗体。

4. 在 "**文件**" 菜单上，单击 "**全部保存**" 以保存工作项。

## <a name="see-also"></a>请参阅
 [测量托管代码的复杂性和可维护性](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)[如何：生成代码度量数据](../code-quality/how-to-generate-code-metrics-data.md)
