---
title: 使用 CheckBox 控件更改工作表格式
description: 了解如何使用 Visual Studio 中的 Office 开发工具创建代码并将其添加到项目。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 28b9f000c2e8517304387e2b203dfa7888b33d64
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97527222"
---
# <a name="walkthrough-change-worksheet-formatting-using-checkbox-controls"></a>演练：使用 CheckBox 控件更改工作表格式
  本演练演示如何使用 Microsoft Office Excel 工作表上的复选框来更改格式设置的基础知识。 你将使用 Visual Studio 中的 Office 开发工具创建代码并将其添加到你的项目。 若要查看已完成示例的结果，请参阅 [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)中的 Excel 控件示例。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 在本演练中，你将学会如何执行以下任务：

- 向工作表添加文本和控件。

- 选择选项时设置文本格式。

- 测试项目。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="create-the-project"></a>创建项目
 在此步骤中，你将使用 Visual Studio 创建一个 Excel 工作簿项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 创建一个名为 **"我的 excel" 格式** 的 Excel 工作簿项目。 请确保已选中 " **创建新文档** "。 有关详细信息，请参阅 [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 将在设计器中打开新的 Excel 工作簿，并将 **我的 Excel 格式设置** 项目添加到 **解决方案资源管理器**。

## <a name="add-text-and-controls-to-the-worksheet"></a>向工作表添加文本和控件
 对于本演练，你将需要 <xref:Microsoft.Office.Tools.Excel.Controls.CheckBox> 在控件中使用三个控件和一些文本 <xref:Microsoft.Office.Tools.Excel.NamedRange> 。

### <a name="to-add-three-check-boxes"></a>添加三个复选框

1. 验证在 Visual Studio 设计器中打开的工作簿，该工作簿是否 `Sheet1` 已打开。

2. 从 "**工具箱**" 的 "**公共控件**" 选项卡中，将 <xref:Microsoft.Office.Tools.Excel.Controls.CheckBox> 控件拖动到 **Sheet1** 中的单元格 **B2** 或附近。

3. 从 " **视图** " 菜单中选择 " **属性** 窗口"。

4. 请确保 "**属性**" 窗口的 "对象名称" 列表框中显示 " **Checkbox1** "，并更改以下属性：

    |properties|值|
    |--------------|-----------|
    |**名称**|**applyBoldFont**|
    |**文本**|**加粗**|

5. 将第二个复选框拖到或附近的单元格 **B4** 上，并更改以下属性：

    |properties|值|
    |--------------|-----------|
    |**名称**|**applyItalicFont**|
    |**文本**|**斜体**|

6. 将第三个复选框拖到单元格 **B6** 上或附近，并更改以下属性：

    |properties|值|
    |--------------|-----------|
    |**名称**|**applyUnderlineFont**|
    |**文本**|**下划线**|

7. 按住 **Ctrl** 键的同时选中所有三个复选框控件。

8. 在 Excel 的 "格式" 选项卡的 "排列" 组中，单击 " **对齐**"，然后单击 " **左对齐**"。

     在您选择的第一个控件的位置，这三个复选框控件在左侧对齐。

     接下来，将控件拖 <xref:Microsoft.Office.Tools.Excel.NamedRange> 到工作表。

    > [!NOTE]
    > 还可以 <xref:Microsoft.Office.Tools.Excel.NamedRange> 通过在 "**名称**" 框中键入 **textFont** 来添加控件。

#### <a name="to-add-text-to-a-namedrange-control"></a>向 NamedRange 控件添加文本

1. 从 "工具箱" 的 " **Excel 控件** " 选项卡中，将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件拖动到单元格 **B9**。

2. 验证 "可编辑" 文本框中是否显示了 " **$B $9** "，并选择了 "单元格 **B9** "。 如果不是，请单击 "单元" **B9** 将其选中。

3. 单击“确定”  。

4. 单元格 **B9** 成为名为的范围 `NamedRange1` 。

    工作表上没有可见的指示，但 `NamedRange1` 显示在 " **名称" 框** 中 (在选择了 "单元格 **B9** " 时) 左侧工作表的上方。

5. 请确保 "**属性**" 窗口的 "对象名称" 列表框中显示 " **NamedRange1** "，并更改以下属性：

   |properties|值|
   |--------------|-----------|
   |**名称**|**textFont**|
   |**Value2**|**单击复选框以更改此文本的格式设置。**|

   接下来，在选择选项时编写代码来设置文本格式。

## <a name="format-the-text-when-an-option-is-selected"></a>选择选项时设置文本格式
 在本部分中，您将编写代码，以便在用户选择格式设置选项时，更改工作表中的文本格式。

### <a name="to-change-formatting-when-a-check-box-is-selected"></a>选中复选框时更改格式设置

1. 右键单击 **Sheet1**，然后单击快捷菜单上的 " **查看代码** "。

2. 将以下代码添加到 <xref:System.Windows.Forms.Control.Click> 该复选框的事件处理程序中 `applyBoldFont` ：

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#7](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#7)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#7](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#7)]

3. 将以下代码添加到 <xref:System.Windows.Forms.Control.Click> 该复选框的事件处理程序中 `applyItalicFont` ：

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#8](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#8)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#8](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#8)]

4. 将以下代码添加到 <xref:System.Windows.Forms.Control.Click> 该复选框的事件处理程序中 `applyUnderlineFont` ：

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#9](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#9)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#9](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#9)]

5. 在 c # 中，必须向事件添加复选框的事件处理程序， <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> 如下所示。 有关创建事件处理程序的信息，请参阅 [如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#10](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#10)]

## <a name="test-the-application"></a>测试应用程序
 你现在可以测试工作簿，以确保在选中或清除复选框时正确设置文本格式。

### <a name="to-test-your-workbook"></a>测试工作簿

1. 按 **F5** 运行项目。

2. 选中或清除复选框。

3. 确认文本格式正确。

## <a name="next-steps"></a>后续步骤
 本演练演示如何在 Excel 工作表中使用复选框和设置文本格式。 以下是接下来可能要执行的一些任务：

- 部署项目。 有关详细信息，请参阅 [使用 ClickOnce 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-clickonce.md)。
- 使用按钮填充文本框。 有关详细信息，请参阅 [演练：使用按钮在工作表的文本框中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)。

## <a name="see-also"></a>另请参阅
- [使用 Excel 的演练](../vsto/walkthroughs-using-excel.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [Office 文档 Windows 窗体控件的限制](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
