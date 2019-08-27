---
title: 使用单选按钮的工作表中更新图表
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, updating using managed controls
- controls [Office development in Visual Studio], updating worksheets
- worksheets, using radio buttons
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 86e289ad8a316f7026d6fda46bb3e424164437fb
ms.sourcegitcommit: 7eb2fb21805d92f085126f3a820ac274f2216b4e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2019
ms.locfileid: "67329014"
---
# <a name="walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons"></a>演练：使用单选按钮更新工作表中的图表
  本演练显示了使用 Microsoft Office Excel 工作表上的单选按钮为用户提供选项之间快速切换的方法的基础知识。 在这种情况下，选项更改图表的样式。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 若要查看已完成的示例，请参阅 Excel 控件示例[Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)。

 本演练阐释了以下任务：

- 向工作表添加一组单选按钮。

- 在选择了某个选项时更改图表样式。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="add-a-chart-to-a-worksheet"></a>将图表添加到工作表
 可以创建自定义现有工作簿的 Excel 工作簿项目。 在此演练中，将将图表添加到工作簿，然后在新的 Excel 解决方案中使用此工作簿。 本演练中的数据源是名为一个工作表**图表数据**。

### <a name="to-add-the-data"></a>若要添加数据

1. 打开 Microsoft Excel。

2. 右键单击**Sheet3**选项卡，然后依次**重命名**快捷菜单上。

3. 向工作表重命名**图表数据**。

4. 添加到以下数据**图表数据**使用 A4 的单元格的左上角和 E8 右下角。

   ||Q1|Q2|Q3|Q4|
   |-|--------|--------|--------|--------|
   |西部|500|550|550|600|
   |东部|600|625|675|700|
   |北部|450|470|490|510|
   |南部|800|750|775|790|

   接下来，将图表添加到第一个工作表以显示数据。

### <a name="to-add-a-chart-in-excel"></a>若要在 Excel 中添加图表

1. 上**插入**选项卡上，在**图表**组中，单击**列**，然后单击**所有图表类型**。

2. 在中**插入图表**对话框中，单击**确定**。

3. 上**设计**选项卡上，在**数据**组中，单击**选择数据**。

4. 在中**选择数据源**对话框中，单击**Chartdata 范围**框，并清除所有默认选择。

5. 在中**图表数据**表中，选择包含的数字，其中包括 A4 中的左上角到 E8 右下角中的单元格的块。

6. 在中**选择数据源**对话框中，单击**确定**。

7. 重新定位图表，以便与单元格的右上角对齐**E2**。

8. 将你的文件保存到驱动器 C 并将其命名**ExcelChart.xlsx**。

9. 退出 Excel。

## <a name="create-a-new-project"></a>创建新项目
 在此步骤中，您将创建基于的 Excel 工作簿项目**ExcelChart**工作簿。

### <a name="to-create-a-new-project"></a>创建新项目

1. 使用名称创建的 Excel 工作簿项目**我的 Excel 图表**。 在向导中，选择**复制现有文档**。

     有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

2. 单击**浏览**按钮，然后浏览到在本演练前面创建的工作簿。

3. 单击 **“确定”** 。

     Visual Studio 设计器中打开新 Excel 工作簿并将添加**我的 Excel 图表**投影到**解决方案资源管理器**。

## <a name="set-properties-of-the-chart"></a>设置图表的属性
 创建使用现有的工作簿的新 Excel 工作簿项目时，自动为所有命名的区域，列表对象和工作簿中的图表创建宿主控件。 可以更改的名称<xref:Microsoft.Office.Tools.Excel.Chart>控件中的使用**属性**窗口。

### <a name="to-change-the-name-of-the-chart-control"></a>若要更改图表控件的名称

1. 选择<xref:Microsoft.Office.Tools.Excel.Chart>设计器中控制和更改中的以下属性**属性**窗口。

    |属性|值|
    |--------------|-----------|
    |**名称**|**dataChart**|
    |**HasLegend**|**false**|

## <a name="add-controls"></a>添加控件
 此工作表使用单选按钮来为用户提供一种方法来快速更改图表样式。 但是，需要是排它性的单选按钮，选择一个按钮后，可以在同一时间选择组中的任何其他按钮。 此行为不会默认发生时向工作表中添加多个单选按钮。

 添加此行为是为了对用户控件，将单选按钮分组的一种方法编写代码针对该用户控件，并将用户控件添加到工作表。

### <a name="to-add-a-user-control"></a>要添加用户控件

1. 选择**我的 Excel 图表**项目中**解决方案资源管理器**。

2. 在 **“项目”** 菜单上，单击 **“添加新项”** 。

3. 在**添加新项**对话框中，单击**用户控件**，将控件**ChartOptions，** 然后单击**添加**。

### <a name="to-add-radio-buttons-to-the-user-control"></a>若要添加到用户控件的单选按钮

1. 如果用户控件不可见的设计器中，双击**ChartOptions**中**解决方案资源管理器**。

2. 从**公共控件**选项卡**工具箱**，将**单选按钮**控制转移到该用户控件，并更改以下属性。

   | 属性 | 值 |
   |----------|------------------|
   | **名称** | **columnChart** |
   | **文本** | **柱形图** |

3. 将第二个单选按钮添加到该用户控件，并更改以下属性。

   | 属性 | 值 |
   |----------|---------------|
   | **名称** | **barChart** |
   | **文本** | **条形图** |

4. 将第三个单选按钮添加到该用户控件，并更改以下属性。

   | 属性 | 值 |
   |----------|----------------|
   | **名称** | **lineChart** |
   | **文本** | **折线图** |

5. 将第四个单选按钮添加到该用户控件，并更改以下属性。

   |属性|值|
   |--------------|-----------|
   |**名称**|**areaBlockChart**|
   |**文本**|**面积图**|

   接下来，编写代码来更新该图表时单击单选按钮。

## <a name="change-the-chart-style-when-a-radio-button-is-selected"></a>单选按钮处于选中状态时更改图表样式
 现在可以添加代码以更改图表样式。 若要执行此操作，创建用户控件上的公共事件，添加一个属性来设置所选内容类型，并创建的事件处理程序`CheckedChanged`的每个单选按钮的事件。

### <a name="to-create-an-event-and-property-on-a-user-control"></a>创建用户控件的事件和属性

1. 在中**解决方案资源管理器**，右键单击用户控件，然后单击**查看代码**。

2. 将代码添加到`ChartOptions`类来创建`SelectionChanged`事件和`Selection`属性。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#13](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#13)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#13](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#13)]

### <a name="to-handle-the-checkedchanged-event-of-the-radio-buttons"></a>若要处理的 CheckedChanged 事件的单选按钮

1. 设置 `CheckedChanged` 单选按钮的 `areaBlockChart` 事件处理程序中的图表类型，然后引发事件。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#14](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#14)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#14](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#14)]

2. 设置 `CheckedChanged` 单选按钮的 `barChart` 事件处理程序中的图表类型。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#15](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#15)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#15](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#15)]

3. 设置 `CheckedChanged` 单选按钮的 `columnChart` 事件处理程序中的图表类型。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#16](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#16)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#16](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#16)]

4. 设置 `CheckedChanged` 单选按钮的 `lineChart` 事件处理程序中的图表类型。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#17](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#17)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#17](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#17)]

5. 在 C# 中，必须为单选按钮添加事件处理程序。 可以将此代码添加到 `ChartOptions` 构造函数中 `InitializeComponent` 调用的下面。 有关如何创建事件处理程序的信息，请参阅[如何：Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-cs[Trin_VstcoreProgrammingControlsExcel#18](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#18)]

## <a name="add-the-user-control-to-the-worksheet"></a>将用户控件添加到工作表
 生成解决方案时，新的用户控件自动添加到**工具箱**。 然后，可以将控件从**工具箱**到工作表。

### <a name="to-add-the-user-control-your-worksheet"></a>若要添加工作表中的用户控件

1. 在 **“生成”** 菜单上，单击 **“生成解决方案”** 。

     **ChartOptions**用户控件添加到**工具箱**。

2. 在中**解决方案资源管理器**，右键单击**Sheet1.vb**或**Sheet1.cs**，然后单击**视图设计器**。

3. 拖动**ChartOptions**控件从**工具箱**到工作表。

     名为的新控件`my_Excel_Chart_ChartOptions1`添加到你的项目。

4. 更改该控件的名称**ChartOptions1**。

## <a name="change-the-chart-type"></a>更改图表类型
 若要更改图表类型，创建的事件处理程序将根据用户控件中选择的选项的样式设置。

### <a name="to-change-the-type-of-chart-that-is-displayed-in-the-worksheet"></a>若要更改的工作表中显示的图表类型

1. 向 `Sheet1` 类添加以下事件处理程序。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#19](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#19)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#19](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#19)]

2. 在 C# 中，必须添加到用户控件的事件处理程序<xref:Microsoft.Office.Tools.Excel.Worksheet.Startup>事件，如下所示。 有关如何创建事件处理程序的信息，请参阅[如何：Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-cs[Trin_VstcoreProgrammingControlsExcel#20](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#20)]

## <a name="test-the-application"></a>测试应用程序
 现在可以测试你的工作簿以验证时选择的单选按钮，该图表的样式设置正确。

### <a name="to-test-your-workbook"></a>测试工作簿

1. 按**F5**运行你的项目。

2. 选择不同的单选按钮。

3. 确认图表样式随所选选项发生了相应的更改。

## <a name="next-steps"></a>后续步骤
 本演练演示在工作表中使用单选按钮和图表样式的基础知识。 以下是接下来可能要执行的一些任务：

- 部署项目。 有关详细信息，请参阅[部署 Office 解决方案](../vsto/deploying-an-office-solution.md)。

- 使用按钮填充文本框。 有关详细信息，请参见[演练：在使用按钮的工作表中的文本框中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)。

- 更改工作表上通过使用复选框格式设置。 有关详细信息，请参见[演练：使用 CheckBox 控件更改工作表格式设置](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)。

## <a name="see-also"></a>请参阅
- [Excel 用法演练](../vsto/walkthroughs-using-excel.md)
