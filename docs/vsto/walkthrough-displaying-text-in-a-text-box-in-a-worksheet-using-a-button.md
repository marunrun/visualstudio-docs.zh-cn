---
title: 使用按钮在工作表的文本框中显示文本
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- text [Office development in Visual Studio], displaying worksheets
- worksheets, displaying text
- text boxes, displaying text in worksheets
- text [Office development in Visual Studio], text boxes
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b30eea0152b75cdd0869ececac674ee5aeee7933
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "67328706"
---
# <a name="walkthrough-display-text-in-a-text-box-in-a-worksheet-using-a-button"></a>演练：使用按钮在工作表的文本框中显示文本
  本演练演示了在 Microsoft Office Excel 工作表上使用按钮和文本框的基础知识，以及如何使用 Visual Studio 中的 Office 开发工具创建 Excel 项目。 若要查看已完成示例的结果，请参阅 [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)中的 Excel 控件示例。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 在本演练中，你将学会如何执行以下任务：

- 向工作表添加控件。

- 在单击按钮时填充文本框。

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

1. 使用 " **我的 excel" 按钮**创建一个 Excel 工作簿项目。 请确保已选中 " **创建新文档** "。 有关详细信息，请参阅 [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 将在设计器中打开新的 Excel 工作簿，并将 " **我的 excel" 按钮** 项目添加到 **解决方案资源管理器**。

## <a name="add-controls-to-the-worksheet"></a>向工作表添加控件
 对于本演练，您将需要第一个工作表上的按钮和文本框。

### <a name="to-add-a-button-and-a-text-box"></a>添加一个按钮和一个文本框

1. 验证是否已在 Visual Studio 设计器中打开 " **我的 Excel Button.xlsx** 工作簿"，并 `Sheet1` 显示。

2. 从 "工具箱" 的 " **公共控件** " 选项卡中，将拖动 <xref:Microsoft.Office.Tools.Excel.Controls.TextBox> 到 `Sheet1` 。

3. 从 " **视图** " 菜单中选择 " **属性窗口**"。

4. 确保 **TextBox1** 在 " **属性** " 窗口下拉框中可见，并将文本框的 " **名称** " 属性 **更改为 "** 显示文本"。

5. 将一个 " **按钮** " 控件拖到上 `Sheet1` ，然后更改以下属性：

   |属性|值|
   |--------------|-----------|
   |**名称**|**insertText**|
   |**Text**|**插入文本**|

   现在，编写在单击按钮时要运行的代码。

## <a name="populate-the-text-box-when-the-button-is-clicked"></a>单击按钮时填充文本框
 每次用户单击该按钮时， **Hello World！** 追加到文本框中。

### <a name="to-write-to-the-text-box-when-the-button-is-clicked"></a>在单击按钮时写入文本框

1. 在 **解决方案资源管理器**中，右键单击 **Sheet1**，然后单击快捷菜单上的 " **查看代码** "。

2. 将以下代码添加到 <xref:System.Windows.Forms.Control.Click> 按钮的事件处理程序中：

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#11](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#11)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#11](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#11)]

3. 在 c # 中，必须向事件添加事件处理程序，如下 <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> 所示。 有关创建事件处理程序的信息，请参阅 [如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#12](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#12)]

## <a name="test-the-application"></a>测试应用程序
 你现在可以测试工作簿，确保消息 **Hello World！** 当您单击按钮时，显示在文本框中。

### <a name="to-test-your-workbook"></a>测试工作簿

1. 按 **F5** 运行项目。

2. 单击按钮。

3. 确认 **Hello World！** 出现在文本框中。

## <a name="next-steps"></a>后续步骤
 本演练演示在 Excel 工作表上使用按钮和文本框的基础知识。 以下是接下来可能要执行的一些任务：

- 部署项目。 有关详细信息，请参阅 [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)。

- 使用复选框来更改格式设置。 有关详细信息，请参阅 [演练：使用 CheckBox 控件更改工作表格式](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)。

## <a name="see-also"></a>另请参阅
- [如何：向 Office 文档添加 Windows 窗体控件](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [使用 Excel 的演练](../vsto/walkthroughs-using-excel.md)
- [Office 文档 Windows 窗体控件的限制](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
