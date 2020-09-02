---
title: 使用单选按钮更新工作表中的图表
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
ms.openlocfilehash: e63d7d09a09fe4c051d8137428fdae90490cbae5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "88238811"
---
# <a name="walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons"></a>演练：使用单选按钮更新工作表中的图表
  本演练演示如何在 Microsoft Office Excel 工作表上使用单选按钮，以使用户能够在两个选项之间快速切换。 在这种情况下，选项更改图表的样式。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 若要查看已完成示例的结果，请参阅 [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)中的 Excel 控件示例。

 本演练演示以下任务：

- 向工作表添加一组单选按钮。

- 在选择了某个选项时更改图表样式。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="add-a-chart-to-a-worksheet"></a>向工作表添加图表
 您可以创建自定义现有工作簿的 Excel 工作簿项目。 在本演练中，您将向工作簿添加一个图表，然后在新的 Excel 解决方案中使用此工作簿。 此演练中的数据源是一个名为 " **图表" 的数据**工作表。

### <a name="to-add-the-data"></a>添加数据

1. 打开 Microsoft Excel。

2. 右键单击 " **Sheet3** " 选项卡，然后单击快捷菜单上的 " **重命名** "。

3. 将工作表重命名为 " **图表数据**"。

4. 将以下数据添加到单元格 A4 为左上角的 **图表** ，并 E8 右下角。

   |区域/季度|Q1|Q2|Q3|Q4|
   |-|--------|--------|--------|--------|
   |West|500|550|550|600|
   |东部|600|625|675|700|
   |北部|450|470|490|510|
   |南部|800|750|775|790|

   接下来，将图表添加到第一个工作表以显示数据。

### <a name="to-add-a-chart-in-excel"></a>在 Excel 中添加图表

1. 在 " **插入** " 选项卡上的 " **图表** " 组中，单击 " **列**"，然后单击 " **所有图表类型**"。

2. 在 " **插入图表** " 对话框中，单击 **"确定"**。

3. 在 " **设计** " 选项卡上的 " **数据** " 组中，单击 " **选择数据**"。

4. 在 " **选择数据源** " 对话框中，单击 " **chartdata.zip" 范围** 框，并清除任何默认选择。

5. 在 " **图表数据** " 工作表中，选择包含数字的单元格块，其中包含从左上角到右下角 E8 的 A4。

6. 在 " **选择数据源** " 对话框中，单击 **"确定"**。

7. 重新定位图表，使右上角与单元格 **E2**对齐。

8. 将文件保存到驱动器 C，并将其命名 **ExcelChart.xlsx**。

9. 退出 Excel。

## <a name="create-a-new-project"></a>创建新项目
 在此步骤中，你将基于 **ExcelChart** 工作簿创建一个 Excel 工作簿项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 创建一个 Excel 工作簿项目，其名称为 **"我的 Excel Chart**"。 在向导中，选择 " **复制现有文档**"。

     有关详细信息，请参阅 [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

2. 单击 " **浏览** " 按钮，浏览到本演练前面部分创建的工作簿。

3. 单击“确定”。

     Visual Studio 将在设计器中打开新的 Excel 工作簿，并将 **我的 Excel 图表** 项目添加到 **解决方案资源管理器**。

## <a name="set-properties-of-the-chart"></a>设置图表的属性
 当您创建使用现有工作簿的新 Excel 工作簿项目时，将自动为该工作簿中的所有命名范围、列表对象和图表创建宿主控件。 您可以 <xref:Microsoft.Office.Tools.Excel.Chart> 使用 " **属性** " 窗口更改控件的名称。

### <a name="to-change-the-name-of-the-chart-control"></a>更改图表控件的名称

1. <xref:Microsoft.Office.Tools.Excel.Chart>在设计器中选择控件，并在 "**属性**" 窗口中更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**dataChart**|
    |**HasLegend**|**false**|

## <a name="add-controls"></a>添加控件
 此工作表使用单选按钮，以使用户能够快速更改图表样式。 但是，单选按钮需要是专用的-当选择一个按钮时，不能同时选择组中的其他按钮。 在将多个单选按钮添加到工作表时，默认情况下不会发生此行为。

 添加此行为的一种方法是将单选按钮分组到用户控件上，在用户控件后面编写代码，然后将用户控件添加到工作表。

### <a name="to-add-a-user-control"></a>要添加用户控件

1. 在**解决方案资源管理器**中选择 "**我的 Excel Chart** " 项目。

2. 在 **“项目”** 菜单上，单击 **“添加新项”**。

3. 在 " **添加新项** " 对话框中，单击 " **用户控件**"，将控件命名为 " **ChartOptions"，** 然后单击 " **添加**"。

### <a name="to-add-radio-buttons-to-the-user-control"></a>向用户控件添加单选按钮

1. 如果用户控件在设计器中不可见，请在**解决方案资源管理器**中双击 " **ChartOptions** "。

2. 从 "**工具箱**" 的 "**公共控件**" 选项卡中，将**单选按钮**控件拖到用户控件，并更改以下属性。

   | 属性 | 值 |
   |----------|------------------|
   | **名称** | **columnChart** |
   | **Text** | **柱形图** |

3. 将第二个单选按钮添加到用户控件，并更改以下属性。

   | 属性 | 值 |
   |----------|---------------|
   | **名称** | **barChart** |
   | **Text** | **条形图** |

4. 将第三个单选按钮添加到用户控件，并更改以下属性。

   | 属性 | 值 |
   |----------|----------------|
   | **名称** | **lineChart** |
   | **Text** | **折线图** |

5. 将第四个单选按钮添加到用户控件，并更改以下属性。

   |属性|值|
   |--------------|-----------|
   |**名称**|**areaBlockChart**|
   |**Text**|**面积图**|

   接下来，在单击单选按钮时编写代码以更新图表。

## <a name="change-the-chart-style-when-a-radio-button-is-selected"></a>选中单选按钮时更改图表样式
 现在，您可以添加代码以更改图表样式。 为此，请在用户控件上创建一个公共事件，添加一个属性以设置选择类型，并为 `CheckedChanged` 每个单选按钮的事件创建一个事件处理程序。

### <a name="to-create-an-event-and-property-on-a-user-control"></a>创建用户控件的事件和属性

1. 在 **解决方案资源管理器**中，右键单击用户控件，然后单击 " **查看代码**"。

2. 向类添加代码 `ChartOptions` 以创建 `SelectionChanged` 事件和 `Selection` 属性。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#13](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#13)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#13](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#13)]

### <a name="to-handle-the-checkedchanged-event-of-the-radio-buttons"></a>处理单选按钮的 CheckedChanged 事件

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

5. 在 C# 中，必须为单选按钮添加事件处理程序。 可以将此代码添加到 `ChartOptions` 构造函数中 `InitializeComponent` 调用的下面。 有关如何创建事件处理程序的信息，请参阅 [如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-cs[Trin_VstcoreProgrammingControlsExcel#18](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#18)]

## <a name="add-the-user-control-to-the-worksheet"></a>将用户控件添加到工作表
 生成解决方案时，新的用户控件将自动添加到 " **工具箱**"。 然后，可以将该控件从 " **工具箱** " 拖动到工作表中。

### <a name="to-add-the-user-control-your-worksheet"></a>向工作表添加用户控件

1. 在“生成”菜单中，单击“生成解决方案”。

     将 **ChartOptions** 用户控件添加到 " **工具箱**"。

2. 在 **解决方案资源管理器**中，右键单击 " **Sheet1** " 或 " **Sheet1.cs**"，然后单击 " **视图设计器**"。

3. 将 **ChartOptions** 控件从 **工具箱** 拖到工作表中。

     名为的新控件 `my_Excel_Chart_ChartOptions1` 将添加到你的项目中。

4. 将控件的名称更改为 **ChartOptions1**。

## <a name="change-the-chart-type"></a>更改图表类型
 若要更改图表类型，请创建一个事件处理程序，该事件处理程序根据用户控件中选定的选项设置样式。

### <a name="to-change-the-type-of-chart-that-is-displayed-in-the-worksheet"></a>更改工作表中显示的图表的类型

1. 向 `Sheet1` 类添加以下事件处理程序。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#19](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#19)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#19](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#19)]

2. 在 c # 中，必须为用户控件添加事件处理程序，如下 <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> 所示。 有关如何创建事件处理程序的信息，请参阅 [如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-cs[Trin_VstcoreProgrammingControlsExcel#20](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#20)]

## <a name="test-the-application"></a>测试应用程序
 你现在可以测试工作簿，以确保在你选择单选按钮时正确地设计图表的样式。

### <a name="to-test-your-workbook"></a>测试工作簿

1. 按 **F5** 运行项目。

2. 选择不同的单选按钮。

3. 确认图表样式随所选选项发生了相应的更改。

## <a name="next-steps"></a>后续步骤
 本演练演示在工作表上使用单选按钮和图表样式的基础知识。 以下是接下来可能要执行的一些任务：

- 部署项目。 有关详细信息，请参阅 [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)。

- 使用按钮填充文本框。 有关详细信息，请参阅 [演练：使用按钮在工作表的文本框中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)。

- 通过使用复选框更改工作表的格式设置。 有关详细信息，请参阅 [演练：使用 CheckBox 控件更改工作表格式](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)。

## <a name="see-also"></a>另请参阅
- [使用 Excel 的演练](../vsto/walkthroughs-using-excel.md)
