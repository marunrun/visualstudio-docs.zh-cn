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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b53e6a5c7ce65675037aac8c6fc4812f895d3b7b
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65703713"
---
# <a name="working-with-code-metrics-data"></a>使用代码度量数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**代码度量结果**窗口将显示生成的代码度量值分析的数据。 代码度量数据值的详细信息，请参阅[代码度量值](../code-quality/code-metrics-values.md)。  
  
 本主题包含以下各节：  
  
- [Code Metrics Results Window](../code-quality/working-with-code-metrics-data.md#BKMK_CodeMetricsResultsWindow)  
  
- [显示代码度量结果](../code-quality/working-with-code-metrics-data.md#BKMK_DisplayingCodeMetricsResults)  
  
- [筛选代码度量结果](../code-quality/working-with-code-metrics-data.md#BKMK_FilteringCodeMetricsResults)  
  
- [添加、 删除和重新排列的数据列](../code-quality/working-with-code-metrics-data.md#BKMK_AddingRemovingandRearrangingDataColumns)  
  
- [将数据复制到剪贴板或 Excel](../code-quality/working-with-code-metrics-data.md#BKMK_Copying_Data_to_the_Clipboard_or_Excel)  
  
- [创建基于代码度量结果的工作项](../code-quality/working-with-code-metrics-data.md#BKMK_Creating_a_Work_Item_Based_on_Code_Metric_Results)  
  
## <a name="BKMK_CodeMetricsResultsWindow"></a> Code Metrics Results Window  
 **代码度量结果**窗口具有工具栏的顶部和要显示计算的结果的列。  
  
|列|描述|  
|------------|-----------------|  
|**层次结构**|**层次结构**列包含的代码层次结构，您可以展开或折叠以查看所需的详细程度的树视图。 其余列显示计算的结果。 可以隐藏或根据需要排列结果列。|  
|**可维护性**|**可维护性**列包含除数字的结果外的图标。 绿色图标表示相对较高的可维护性。 黄色图标表示了中等程度的可维护性。 红色图标表示较低的可维护性和潜在的问题点。 这些颜色指示符对应于使用 FxCop 规则 AvoidUnmaintainableCode 的严重性类别。 如果可维护性指数低于 10 中，如果索引之间 10 和 20，和既不会引发错误和警告的索引是 20 个以上的警告，此规则将触发错误。 可维护性指数是三个度量值的合成： 圈复杂度、 代码和计算的复杂程度的行。 其值不表示为单位。|  
  
## <a name="BKMK_DisplayingCodeMetricsResults"></a> 显示代码度量结果  
 生成代码度量结果，将自动显示代码度量结果窗口中。 此外可以在任何时候显示窗口。  
  
#### <a name="to-display-the-code-metrics-results-window"></a>若要显示代码度量结果窗口  
  
- 上**分析**菜单上，单击**Windows** ，然后单击**代码度量结果**。  
  
     \- 或 -  
  
- 上**视图**菜单，依次指向**其他 Windows** ，然后单击**代码度量结果**。  
  
     即使不包含任何结果，将显示代码度量结果窗口。  
  
#### <a name="to-view-code-metrics-details"></a>若要查看代码度量值详细信息  
  
- 如果已生成代码度量结果，则展开的树中**层次结构**列。  
  
## <a name="BKMK_FilteringCodeMetricsResults"></a> 筛选代码度量结果  
 您可以筛选结果中显示**代码度量结果**窗口是通过使用顶部的工具栏。 例如，您可能想要查看具有低于 65 可维护性索引的结果。  
  
 **筛选器**下拉列表框中包含的结果列的名称。 定义筛选器时，则将它添加到并进行缩进列表的底部。 该列表可以包含未定义的 10 个最新筛选器。  
  
#### <a name="to-filter-the-code-metrics-results"></a>若要筛选代码度量结果  
  
1. 从**筛选器**列表中，选择的列名称。  
  
2. 在中**Min**，键入要显示的最小值。  
  
3. 在中**最大**，键入要显示的最大值。  
  
4. 单击**应用筛选器**按钮。  
  
5. 若要查看结果详细信息，请展开层次结构树。  
  
## <a name="BKMK_AddingRemovingandRearrangingDataColumns"></a> 添加、 删除和重新排列的数据列  
 您可以添加或删除的结果中的列**代码度量结果**窗口。 此外，以使它们显示在所需的顺序可以重新排列结果列。  
  
#### <a name="to-remove-a-column"></a>若要删除某一列  
  
1. 单击**添加/删除列**按钮。  
  
     \- 或 -  
  
     右键单击任意列标题，然后单击**添加/删除列**。  
  
2. 在中**添加/删除列**对话框中，清除该复选框列想要删除，然后单击**确定**。  
  
#### <a name="to-add-a-previously-removed-column"></a>若要添加先前删除的列  
  
1. 单击**添加/删除列**按钮。  
  
     \- 或 -  
  
     右键单击任意列标题，然后单击**添加/删除列**。  
  
2. 在中**添加/删除列**对话框框中，选中你想要添加，然后单击的列的复选框**确定**。  
  
#### <a name="to-rearrange-columns"></a>若要重新排列列  
  
1. 单击**添加/删除列**按钮。  
  
     \- 或 -  
  
     右键单击任意列标题，然后单击**添加/删除列**。  
  
2. 在中**添加/删除列**对话框框中，选择你想要移动，然后单击向上箭头或向下箭头的列。  
  
3. 当列位于所需的位置时，单击**确定**。  
  
## <a name="BKMK_Copying_Data_to_the_Clipboard_or_Excel"></a> 将数据复制到剪贴板或 Excel  
 可以选择并复制到剪贴板作为文本字符串都包含一行的名称和每个数据列的值为所选的行的代码度量数据。 此外可以单击**在 Microsoft Excel 中打开列表**将所有代码度量结果导出到 Excel 电子表格  
  
## <a name="BKMK_Creating_a_Work_Item_Based_on_Code_Metric_Results"></a> 创建基于代码度量结果的工作项  
 您可以创建[!INCLUDE[esprfound](../includes/esprfound-md.md)]基于的工作项会导致**代码度量结果**窗口。 当创建工作项时，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]会自动输入中的标题**标题**下的字段和代码度量值数据**历史记录**选项卡。  
  
 有关如何创建工作项的详细信息，请参阅[创建工作项&#91;重定向&#93;](https://msdn.microsoft.com/24b2e064-16ac-4bf0-8de4-98a1f48b8c4b)。  
  
#### <a name="to-create-a-work-item-based-on-a-result"></a>若要创建基于某一结果的工作项  
  
1. 右键单击结果。  
  
2. 指向**创建工作项**，然后单击你想要创建的工作项类型 (**Bug**，**任务**，依此类推)。  
  
3. 通过填写所有必填字段来完成工作项窗体。  
  
4. 上**文件**菜单上，单击**全部保存**来保存工作项。  
  
#### <a name="to-create-a-bug-based-on-a-result"></a>若要创建基于某一结果的 bug  
  
1. 单击以选中它的结果。  
  
2. 单击**创建工作项**按钮。  
  
3. 通过填写所有必填字段来完成工作项窗体。  
  
4. 上**文件**菜单上，单击**全部保存**来保存工作项。  
  
## <a name="see-also"></a>请参阅  
 [测量复杂性和可维护性的托管代码](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)   
 [如何：生成代码度量数据](../code-quality/how-to-generate-code-metrics-data.md)
