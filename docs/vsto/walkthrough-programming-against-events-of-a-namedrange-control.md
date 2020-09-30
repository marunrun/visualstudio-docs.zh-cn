---
title: 演练：针对 NamedRange 控件的事件进行编程
titleSuffix: ''
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
ms.openlocfilehash: 2e5ce12e2de8274afd2c27d4ece36529563a6386
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584932"
---
# <a name="walkthrough-program-against-events-of-a-namedrange-control"></a>演练：针对 NamedRange 控件的事件进行编程
  本演练演示如何 <xref:Microsoft.Office.Tools.Excel.NamedRange> 使用 Visual Studio 中的 Office 开发工具将控件添加到 Microsoft Office Excel 工作表并针对其事件进行编程。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 在本演练中，你将学会如何执行以下任务：

- 向 <xref:Microsoft.Office.Tools.Excel.NamedRange> 工作表添加控件。

- 针对 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件事件进行编程。

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

1. 使用名称 **命名范围事件**创建 Excel 工作簿项目。 请确保已选中 " **创建新文档** "。 有关详细信息，请参阅 [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 将在设计器中打开新的 Excel 工作簿，并将 " **我的命名范围事件** " 项目添加到 **解决方案资源管理器**。

## <a name="add-text-and-named-ranges-to-the-worksheet"></a>向工作表添加文本和命名范围
 由于主机控件是扩展的 Office 对象，因此可以采用与添加本机对象相同的方式将其添加到文档中。 例如，可以 <xref:Microsoft.Office.Tools.Excel.NamedRange> 通过打开 " **插入** " 菜单，指向 " **名称**"，然后选择 " **定义**"，将 Excel 控件添加到工作表中。 还可以 <xref:Microsoft.Office.Tools.Excel.NamedRange> 通过将控件从 " **工具箱** " 拖到工作表上来添加控件。

 在此步骤中，您将使用 **工具箱**向工作表添加两个命名范围控件，然后向工作表添加文本。

### <a name="to-add-a-range-to-your-worksheet"></a>向工作表添加范围

1. 验证是否已在 Visual Studio 设计器中打开 " *我的命名范围 Events.xlsx* 工作簿"，并 `Sheet1` 显示。

2. 从 "工具箱" 的 " **Excel 控件** " 选项卡中，将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件拖动到中的单元格 **A1** `Sheet1` 。

     此时将显示 " **添加 NamedRange 控件** " 对话框。

3. 验证 "可编辑" 文本框中是否显示 **$A $1** ，并选中 " **A1** 单元格"。 如果不是，请单击单元格 **A1** 将其选中。

4. 单击“确定”。

     单元格 **A1** 变为名为的范围 `namedRange1` 。 工作表上没有可见的指示，但 `namedRange1` 显示在 " **名称** " 框中 (在选择单元格 **A1** 时) 左侧工作表的上方。

5. 向 <xref:Microsoft.Office.Tools.Excel.NamedRange> 单元格 **B3**添加另一个控件。

6. 验证 "可编辑" 文本框中是否显示了 **$B $3** ，并选中了 "单元格 **B3** "。 如果不是，请单击单元格 **B3** 将其选中。

7. 单击“确定”。

     单元格 **B3** 成为名为的范围 `namedRange2` 。

### <a name="to-add-text-to-your-worksheet"></a>向工作表添加文本

1. 在单元格 **A1**中，键入以下文本：

    **这是 NamedRange 控件的一个示例。**

2. 在) 左侧的单元格 **A3** (中 `namedRange2` ，键入以下文本：

    **事件**

   在下面几节中，你将编写代码，用于将文本插入 `namedRange2` 和修改控件的属性 `namedRange2` 以响应的 <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> 、 <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> 和 <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> 事件 `namedRange1` 。

## <a name="add-code-to-respond-to-the-beforedoubleclick-event"></a>添加代码以响应 BeforeDoubleClick 事件

### <a name="to-insert-text-into-namedrange2-based-on-the-beforedoubleclick-event"></a>基于 BeforeDoubleClick 事件向 NamedRange2 插入文本

1. 在 **解决方案资源管理器**中，右键单击 " **Sheet1** " 或 " **Sheet1.cs** "，然后选择 " **查看代码**"。

2. 添加代码，以便 `namedRange1_BeforeDoubleClick` 事件处理程序如下所示：

     [!code-csharp[Trin_VstcoreHostControlsExcel#24](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#24)]
     [!code-vb[Trin_VstcoreHostControlsExcel#24](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#24)]

3. 在 c # 中，必须添加命名范围的事件处理程序，如下面的事件中所示 <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> 。 有关创建事件处理程序的信息，请参阅 [如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreHostControlsExcel#25](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#25)]

## <a name="add-code-to-respond-to-the-change-event"></a>添加代码以响应更改事件

### <a name="to-insert-text-into-namedrange2-based-on-the-change-event"></a>基于 Change 事件向 namedRange2 插入文本

1. 添加代码，以便 `NamedRange1_Change` 事件处理程序如下所示：

     [!code-csharp[Trin_VstcoreHostControlsExcel#26](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#26)]
     [!code-vb[Trin_VstcoreHostControlsExcel#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#26)]

    > [!NOTE]
    > 因为在 Excel 范围内双击某个单元将进入编辑模式，所以， <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> 当所选内容移到范围之外时，即使没有对文本所做的更改，也将发生事件。

## <a name="add-code-to-respond-to-the-selectionchange-event"></a>添加代码以响应 SelectionChange 事件

### <a name="to-insert-text-into-namedrange2-based-on-the-selectionchange-event"></a>基于 SelectionChange 事件向 namedRange2 插入文本

1. 添加代码，以便 **NamedRange1_SelectionChange** 事件处理程序如下所示：

     [!code-csharp[Trin_VstcoreHostControlsExcel#27](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#27)]
     [!code-vb[Trin_VstcoreHostControlsExcel#27](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#27)]

    > [!NOTE]
    > 由于双击 Excel 范围中的某个单元会导致所选内容移动到该范围内，因此事件发生 <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> 之前发生 <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> 。

## <a name="test-the-application"></a>测试应用程序
 现在，可以测试工作簿，验证 <xref:Microsoft.Office.Tools.Excel.NamedRange> 当引发事件时，将描述控件事件的文本插入到另一个命名范围中。

### <a name="to-test-your-document"></a>测试文档

1. 按 **F5** 运行项目。

2. 将光标置于 `namedRange1` ，并验证是否插入了与事件有关的文本以及是否在 <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> 工作表中插入了注释。

3. 双击 `namedRange1` ，并验证与事件相关的文本 <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> 是否在中插入了红色斜体文本 `namedRange2` 。

4. 在外单击 `namedRange1` 并注意，在退出编辑模式时发生更改事件，即使未对文本进行任何更改。

5. 更改中的文本 `namedRange1` 。

6. 单击 "外部" `namedRange1` ，并验证是否已将 <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> 包含蓝色文本的文本插入到中 `namedRange2` 。

## <a name="next-steps"></a>后续步骤
 此演练演示对控件的事件进行编程的基本知识 <xref:Microsoft.Office.Tools.Excel.NamedRange> 。 下面是一个可能会接下来执行的任务：

- 部署项目。 有关详细信息，请参阅 [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)。

## <a name="see-also"></a>另请参阅
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [使用扩展对象实现 Excel 自动化](../vsto/automating-excel-by-using-extended-objects.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [如何：调整 NamedRange 控件的大小](../vsto/how-to-resize-namedrange-controls.md)
- [如何：向工作表添加 NamedRange 控件](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)
