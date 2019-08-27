---
title: 演练：针对 NamedRange 控件的事件进行编程
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, programming against events
- worksheets, changing cell values
- NamedRange control, events
- worksheets, events
- worksheets, automating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9b510e7464708891db0cab23d61cb22896a74602
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446918"
---
# <a name="walkthrough-program-against-events-of-a-namedrange-control"></a>演练：针对 NamedRange 控件的事件进行编程
  本演练演示如何添加<xref:Microsoft.Office.Tools.Excel.NamedRange>对 Microsoft Office Excel 工作表和对其事件通过使用 Visual Studio 中的 Office 开发工具进行编程控制。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 在本演练中，你将学会如何执行以下任务：

- 添加<xref:Microsoft.Office.Tools.Excel.NamedRange>向工作表中的控件。

- 对其进行编程<xref:Microsoft.Office.Tools.Excel.NamedRange>控件事件。

- 测试您的项目。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="create-the-project"></a>创建项目
 在此步骤中，将创建使用 Visual Studio 的 Excel 工作簿项目。

### <a name="to-create-a-new-project"></a>创建新项目

1. 使用名称创建的 Excel 工作簿项目**我的名为范围活动**。 请确保**创建一个新文档**处于选中状态。 有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 设计器中打开新 Excel 工作簿并将添加**我的名为范围活动**投影到**解决方案资源管理器**。

## <a name="add-text-and-named-ranges-to-the-worksheet"></a>添加文本和指定到工作表范围
 由于宿主控件扩展 Office 对象后，可以将它们添加到你的文档以相同方式添加本机对象。 例如，可以添加 Excel<xref:Microsoft.Office.Tools.Excel.NamedRange>到通过打开工作表控件**插入**菜单，指向**名称**，然后选择**定义**。 您还可以添加<xref:Microsoft.Office.Tools.Excel.NamedRange>通过将其从控件**工具箱**到工作表上。

 在此步骤中，将两个命名的范围控件添加到工作表使用**工具箱**，然后将文本添加到工作表。

### <a name="to-add-a-range-to-your-worksheet"></a>若要添加到工作表范围

1. 确认*我的名为范围 Events.xlsx*工作簿是在 Visual Studio 设计器中，打开与`Sheet1`显示。

2. 从**Excel 控件**选项卡的工具箱拖动<xref:Microsoft.Office.Tools.Excel.NamedRange>单元格的控件**A1**中`Sheet1`。

     **添加 NamedRange 控件**对话框随即出现。

3. 确认 **$A 1 美元**将出现在可编辑的文本框，然后该单元格**A1**处于选中状态。 如果不存在，请单击单元格**A1**以将其选中。

4. 单击 **“确定”**。

     单元格**A1**变得名为一个范围`namedRange1`。 在工作表上没有可见的指示，但`namedRange1`将出现在**名称**框 （位于左侧和右侧的工作表的正上方） 单元格时**A1**处于选中状态。

5. 添加另一个<xref:Microsoft.Office.Tools.Excel.NamedRange>控制对单元格**B3**。

6. 确认 **$B 3 美元**将出现在可编辑的文本框，然后该单元格**B3**处于选中状态。 如果不存在，请单击单元格**B3**以将其选中。

7. 单击 **“确定”**。

     单元格**B3**变得名为一个范围`namedRange2`。

### <a name="to-add-text-to-your-worksheet"></a>若要将文本添加到您的工作表

1. 在单元格中**A1**，键入以下文本：

    **这是 NamedRange 控件的一个示例。**

2. 在单元格中**A3** (左侧的`namedRange2`)，键入以下文本：

    **事件：**

   在以下部分中，您将编写代码将插入到文本`namedRange2`，并修改的属性`namedRange2`控件以响应<xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick>， <xref:Microsoft.Office.Tools.Excel.NamedRange.Change>，和<xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange>事件的`namedRange1`。

## <a name="add-code-to-respond-to-the-beforedoubleclick-event"></a>添加代码以响应 BeforeDoubleClick 事件

### <a name="to-insert-text-into-namedrange2-based-on-the-beforedoubleclick-event"></a>若要将文本插入到 NamedRange2 基于 BeforeDoubleClick 事件

1. 在中**解决方案资源管理器**，右键单击**Sheet1.vb**或**Sheet1.cs** ，然后选择**查看代码**。

2. 添加代码以便`namedRange1_BeforeDoubleClick`事件处理程序看起来如下所示：

     [!code-csharp[Trin_VstcoreHostControlsExcel#24](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#24)]
     [!code-vb[Trin_VstcoreHostControlsExcel#24](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#24)]

3. 在 C# 中，您必须添加命名范围的事件处理程序，如中所示<xref:Microsoft.Office.Tools.Excel.Worksheet.Startup>下面的事件。 有关创建事件处理程序的信息，请参阅[如何：Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreHostControlsExcel#25](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#25)]

## <a name="add-code-to-respond-to-the-change-event"></a>添加代码以响应更改事件

### <a name="to-insert-text-into-namedrange2-based-on-the-change-event"></a>若要将文本插入到 namedRange2 基于更改事件

1. 添加代码以便`NamedRange1_Change`事件处理程序看起来如下所示：

     [!code-csharp[Trin_VstcoreHostControlsExcel#26](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#26)]
     [!code-vb[Trin_VstcoreHostControlsExcel#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#26)]

    > [!NOTE]
    > 双击 Excel 区域中的单元格进入编辑模式，因为<xref:Microsoft.Office.Tools.Excel.NamedRange.Change>所选内容移动的范围之外，即使未文本发生更改时发生事件。

## <a name="add-code-to-respond-to-the-selectionchange-event"></a>添加代码以响应 SelectionChange 事件

### <a name="to-insert-text-into-namedrange2-based-on-the-selectionchange-event"></a>若要将文本插入到 namedRange2 基于 SelectionChange 事件

1. 添加代码以便**NamedRange1_SelectionChange**事件处理程序看起来如下所示：

     [!code-csharp[Trin_VstcoreHostControlsExcel#27](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#27)]
     [!code-vb[Trin_VstcoreHostControlsExcel#27](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#27)]

    > [!NOTE]
    > 双击 Excel 区域中的单元格使所选内容将移到范围，因为<xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange>事件之前发生<xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick>事件发生。

## <a name="test-the-application"></a>测试应用程序
 现在可以测试你的工作簿以验证该文本描述的事件<xref:Microsoft.Office.Tools.Excel.NamedRange>引发事件时，将控件插入到另一个命名范围。

### <a name="to-test-your-document"></a>测试文档

1. 按**F5**运行你的项目。

2. 将光标置于`namedRange1`，并确认文本有关<xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange>插入事件和注释插入到表。

3. 双击内部`namedRange1`，并确认文本有关<xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick>中的红色斜体文本插入事件`namedRange2`。

4. 外单击`namedRange1`并记下更改事件发生时退出编辑模式，即使没有做任何更改的文本。

5. 更改中的文本`namedRange1`。

6. 单击之外`namedRange1`，并确认文本有关<xref:Microsoft.Office.Tools.Excel.NamedRange.Change>事件插入到蓝色文本与`namedRange2`。

## <a name="next-steps"></a>后续步骤
 本演练显示了对事件的编程的基础知识<xref:Microsoft.Office.Tools.Excel.NamedRange>控件。 下面是可能出现的下一任务：

- 部署项目。 有关详细信息，请参阅[部署 Office 解决方案](../vsto/deploying-an-office-solution.md)。

## <a name="see-also"></a>请参阅
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [通过使用扩展的对象自动化 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [如何：调整 NamedRange 控件的大小](../vsto/how-to-resize-namedrange-controls.md)
- [如何：向工作表添加 NamedRange 控件](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [如何：Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)
