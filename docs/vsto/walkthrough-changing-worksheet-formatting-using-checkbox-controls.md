---
title: 更改工作表格式设置使用 CheckBox 控件
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, changing formatting using managed controls
- worksheets, check box controls
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 42d2c46f6fd61d74476933cfda3dea8c62b00c95
ms.sourcegitcommit: 7eb2fb21805d92f085126f3a820ac274f2216b4e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2019
ms.locfileid: "67328700"
---
# <a name="walkthrough-change-worksheet-formatting-using-checkbox-controls"></a>演练：更改工作表格式设置使用 CheckBox 控件
  本演练显示了使用 Microsoft Office Excel 工作表上的复选框来更改格式设置基础的知识。 将使用 Visual Studio 中的 Office 开发工具创建并将代码添加到你的项目。 若要查看已完成的示例，请参阅 Excel 控件示例[Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 在本演练中，你将学会如何执行以下任务：

- 将文本和控件添加到工作表。

- 设置文本格式时选择一个选项。

- 测试您的项目。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="create-the-project"></a>创建项目
 在此步骤中，将通过使用 Visual Studio 中创建的 Excel 工作簿项目。

### <a name="to-create-a-new-project"></a>创建新项目

1. 使用名称创建的 Excel 工作簿项目**我 Excel 格式设置**。 请确保**创建一个新文档**处于选中状态。 有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 设计器中打开新 Excel 工作簿并将添加**我 Excel 格式设置**投影到**解决方案资源管理器**。

## <a name="add-text-and-controls-to-the-worksheet"></a>将文本和控件添加到工作表
 对于本演练中，您将需要三个<xref:Microsoft.Office.Tools.Excel.Controls.CheckBox>控件和中的某些文本<xref:Microsoft.Office.Tools.Excel.NamedRange>控件。

### <a name="to-add-three-check-boxes"></a>若要添加三个复选框

1. 验证工作簿是在 Visual Studio 设计器，并打开`Sheet1`处于打开状态。

2. 从**公共控件**选项卡**工具箱**，拖动<xref:Microsoft.Office.Tools.Excel.Controls.CheckBox>控制到或接近单元格**B2**中**Sheet1**。

3. 从**视图**菜单中，选择**属性**窗口。

4. 确保**Checkbox1**是可见的对象名称列表框中**属性**窗口中，并更改以下属性：

    |属性|值|
    |--------------|-----------|
    |**名称**|**applyBoldFont**|
    |**文本**|**加粗**|

5. 将第二个复选框，或其附近单元格**B4**并更改以下属性：

    |属性|值|
    |--------------|-----------|
    |**名称**|**applyItalicFont**|
    |**文本**|**斜体**|

6. 拖动第三个复选框，或其附近单元格**B6**并更改以下属性：

    |属性|值|
    |--------------|-----------|
    |**名称**|**applyUnderlineFont**|
    |**文本**|**用下划线标出**|

7. 选择所有三个复选框控件按住**Ctrl**密钥。

8. 在 Excel 中的格式选项卡的排列组中，单击**对齐**，然后单击**左对齐**。

     三个复选框控件上的所选的第一个控件的位置的左侧对齐。

     接下来，将拖动<xref:Microsoft.Office.Tools.Excel.NamedRange>到工作表中的控件。

    > [!NOTE]
    > 您还可以添加<xref:Microsoft.Office.Tools.Excel.NamedRange>通过键入控件**textFont**到**名称**框。

#### <a name="to-add-text-to-a-namedrange-control"></a>若要将文本添加到 NamedRange 控件

1. 从**Excel 控件**选项卡的工具箱拖动<xref:Microsoft.Office.Tools.Excel.NamedRange>单元格的控件**B9**。

2. 确认 **$B$ 9**将出现在可编辑的文本框，然后该单元格**B9**处于选中状态。 如果不存在，请单击单元格**B9**以将其选中。

3. 单击 **“确定”** 。

4. 单元格**B9**变得名为一个范围`NamedRange1`。

    在工作表上没有可见的指示，但`NamedRange1`将出现在**名称框**（只是工作表的上方左侧和右侧） 单元格时**B9**处于选中状态。

5. 确保**NamedRange1**是可见的对象名称列表框中**属性**窗口中，并更改以下属性：

   |属性|值|
   |--------------|-----------|
   |**名称**|**textFont**|
   |**Value2**|**单击复选框来更改此文本的格式设置。**|

   接下来，编写代码以设置文本格式时选择一个选项。

## <a name="format-the-text-when-an-option-is-selected"></a>设置文本格式时选择一个选项
 在本部分中，将编写代码，以便当用户选择一种格式化选项，更改在工作表中的文本的格式。

### <a name="to-change-formatting-when-a-check-box-is-selected"></a>若要更改格式设置时复选框已选中

1. 右键单击**Sheet1**，然后单击**查看代码**快捷菜单上。

2. 将以下代码添加到<xref:System.Windows.Forms.Control.Click>事件处理程序`applyBoldFont`复选框：

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#7](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#7)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#7](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#7)]

3. 将以下代码添加到<xref:System.Windows.Forms.Control.Click>事件处理程序`applyItalicFont`复选框：

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#8](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#8)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#8](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#8)]

4. 将以下代码添加到<xref:System.Windows.Forms.Control.Click>事件处理程序`applyUnderlineFont`复选框：

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#9](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#9)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#9](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#9)]

5. 在 C# 中，必须添加到对应的复选框为事件处理程序<xref:Microsoft.Office.Tools.Excel.Worksheet.Startup>事件，如下所示。 有关创建事件处理程序的信息，请参阅[如何：Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#10](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#10)]

## <a name="test-the-application"></a>测试应用程序
 现在可以测试你的工作簿，以确保文本的格式正确，当您选择或清除复选框。

### <a name="to-test-your-workbook"></a>测试工作簿

1. 按**F5**运行你的项目。

2. 选中或清除复选框。

3. 确认文本已正确设置格式。

## <a name="next-steps"></a>后续步骤
 本演练显示了使用复选框和设置 Excel 工作表上的文本格式基础的知识。 以下是接下来可能要执行的一些任务：

- 部署项目。 有关详细信息，请参阅[通过使用 ClickOnce 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-clickonce.md)。
- 使用按钮填充文本框。 有关详细信息，请参见[演练：在使用按钮的工作表中的文本框中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)。

## <a name="see-also"></a>请参阅
- [Excel 用法演练](../vsto/walkthroughs-using-excel.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [Office 文档上的 Windows 窗体控件的限制](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
