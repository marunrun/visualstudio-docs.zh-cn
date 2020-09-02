---
title: 演练：使用单选按钮更新文档中的图表
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], updating using controls
- controls [Office development in Visual Studio], updating documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 88f7bb81557db813912fe4470e63b8d52c0c9371
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62981044"
---
# <a name="walkthrough-update-a-chart-in-a-document-using-radio-buttons"></a>演练：使用单选按钮更新文档中的图表
  此演练演示如何使用 Microsoft Office Word 文档级自定义中的单选按钮，为用户提供在文档中选择图表样式的选项。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 本演练演示以下任务：

- 在文档级项目中，在设计时向文档中添加图表。

- 通过将单选按钮添加到用户控件来对它们进行分组。

- 在选择了某个选项时更改图表样式。

  若要查看已完成示例的结果，请参阅 [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)中的 Word 控件示例。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 或 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-the-project"></a>创建项目
 第一步是创建 Word 文档项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 创建一个名为 **"我的图表" 选项**的 Word 文档项目。 在向导中，选择 " **创建新文档**"。 有关详细信息，请参阅 [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 将在设计器中打开新的 Word 文档，并将 " **我的图表选项** " 项目添加到 **解决方案资源管理器**。

## <a name="add-a-chart-to-the-document"></a>向文档中添加图表

### <a name="to-add-a-chart"></a>添加图表

1. 在 Visual Studio 设计器承载的 Word 文档中，单击功能区上的 " **插入** " 选项卡。

2. 在 " **文本** " 组中，单击 " **插入对象** " 下拉按钮，然后单击 " **对象**"。

     此时将打开 " **对象** " 对话框。

3. 在 **"新建" 选项卡**上的 "**对象类型**" 列表中，选择**Microsoft Graph 图表**，然后单击 **"确定"**。

     将在文档中的插入点处添加一个图表，并且 " **数据表** " 窗口将显示某些默认数据。

4. 关闭 **"数据表** " 窗口以接受图表中的默认值，然后在文档内单击以将焦点移到图表之外。

5. 右键单击图表，然后单击 " **设置对象格式**"。

6. 在 "**设置对象格式**" 对话框的 "**布局**" 选项卡上，选择 "**正方形**" 并单击 **"确定"**。

## <a name="add-a-user-control-to-the-project"></a>将用户控件添加到项目中
 文档上的单选按钮默认情况下不互相排斥。 通过将这些按钮添加到用户控件中，然后编写代码来控制选择，可使这些按钮正常工作。

### <a name="to-add-a-user-control"></a>要添加用户控件

1. 在**解决方案资源管理器**中选择 "**我的图表选项**" 项目。

2. 在 **“项目”** 菜单上，单击 **“添加新项”**。

3. 在 " **添加新项** " 对话框中，单击 " **用户控件**"，将控件命名为 " **ChartOptions"，** 然后单击 " **添加**"。

### <a name="to-add-windows-form-controls-to-the-user-control"></a>向用户控件添加 Windows 窗体控件

1. 如果用户控件在设计器中不可见，请在**解决方案资源管理器**中双击 " **ChartOptions** "。

2. 从 "**工具箱**" 的 "**公共控件**" 选项卡中，将第一个**单选按钮**控件拖到用户控件，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**columnChart**|
    |**Text**|**柱形图**|

3. 将第二个 **单选按钮** 添加到用户控件，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**barChart**|
    |**Text**|**条形图**|

4. 将第三个 **单选按钮** 添加到用户控件，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**lineChart**|
    |**Text**|**折线图**|

5. 将第四个 **单选按钮** 添加到用户控件，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**areaBlockChart**|
    |**Text**|**面积图**|

## <a name="add-references"></a>添加引用
 若要从文档中的用户控件访问图表，您必须对 `Microsoft.Office.Interop.Graph` 项目中的程序集具有引用。

### <a name="to-add-a-reference-to-the-microsoftofficeinteropgraph-assembly"></a>添加对 Microsoft.Office.Interop.Graph 程序集的引用

1. 在“项目”菜单上，单击“添加引用”。

     此时将显示“添加引用”对话框。

2. 在 " **.net** " 选项卡上 **，选择 ""，然后** 单击 **"确定"**。 选择该程序集的 14.0.0.0 版。

## <a name="change-the-chart-style-when-a-radio-button-is-selected"></a>选中单选按钮时更改图表样式
 若要使这些按钮正常工作，请创建用户控件的公共事件，添加属性以设置选择类型，并为每个单选按钮的 `CheckedChanged` 事件创建过程。

### <a name="to-create-an-event-and-property-on-a-user-control"></a>创建用户控件的事件和属性

1. 在 **解决方案资源管理器**中，右键单击用户控件，然后单击 " **查看代码**"。

2. 向 `SelectionChanged` 类添加代码以创建 `Selection` 事件和 `ChartOptions` 属性。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#9](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#9)]
     [!code-vb[Trin_VstcoreProgrammingControlsWord#9](../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb#9)]

### <a name="to-handle-the-checkedchange-event-of-the-radio-buttons"></a>处理单选按钮的 CheckedChange 事件

1. 设置 `CheckedChanged` 单选按钮的 `areaBlockChart` 事件处理程序中的图表类型，然后引发事件。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#10](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#10)]
     [!code-vb[Trin_VstcoreProgrammingControlsWord#10](../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb#10)]

2. 设置 `CheckedChanged` 单选按钮的 `barChart` 事件处理程序中的图表类型。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#11](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#11)]
     [!code-vb[Trin_VstcoreProgrammingControlsWord#11](../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb#11)]

3. 设置 `CheckedChanged` 单选按钮的 `columnChart` 事件处理程序中的图表类型。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#12](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#12)]
     [!code-vb[Trin_VstcoreProgrammingControlsWord#12](../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb#12)]

4. 设置 `CheckedChanged` 单选按钮的 `lineChart` 事件处理程序中的图表类型。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#13](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#13)]
     [!code-vb[Trin_VstcoreProgrammingControlsWord#13](../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb#13)]

5. 在 C# 中，必须为单选按钮添加事件处理程序。 可以将此代码添加到 `ChartOptions` 构造函数中 `InitializeComponent` 调用的下面。 有关创建事件处理程序的信息，请参阅 [如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#14](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#14)]

## <a name="add-the-user-control-to-the-document"></a>向文档添加用户控件
 生成解决方案时，新的用户控件将自动添加到 " **工具箱**"。 然后，可以将该控件从 " **工具箱** " 拖动到文档中。

### <a name="to-add-the-user-control-your-document"></a>向文档添加用户控件

1. 在“生成”菜单中，单击“生成解决方案”。

     将 **ChartOptions** 用户控件添加到 " **工具箱**"。

2. 在 **解决方案资源管理器**中，右键单击 " **ThisDocument** " 或 " **ThisDocument.cs**"，然后单击 " **视图设计器**"。

3. 将 `ChartOptions` 控件从 " **工具箱** " 拖动到文档。

     在 " **属性** " 窗口中，为刚添加到文档中的控件命名  `ChartOptions1` 。

## <a name="change-the-chart-type"></a>更改图表类型
 创建一个事件处理程序，以根据在用户控件中选择的选项更改图表类型。

### <a name="to-change-the-type-of-chart-that-is-displayed-in-the-document"></a>更改文档中显示的图表类型

1. 向 `ThisDocument` 类添加以下事件处理程序。

     [!code-vb[Trin_VstcoreProgrammingControlsWord#15](../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb#15)]
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#15](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#15)]

2. 在 C# 中，必须向 <xref:Microsoft.Office.Tools.Word.Document.Startup> 事件添加用户控件的事件处理程序。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#16](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#16)]

## <a name="test-the-application"></a>测试应用程序
 现在，你可以对文档进行测试，以确保选择单选按钮时能正确更新图表样式。

### <a name="to-test-your-document"></a>测试文档

1. 按 **F5** 运行项目。

2. 选择不同的单选按钮。

3. 确认图表样式随所选选项发生了相应的更改。

## <a name="next-steps"></a>后续步骤
 以下是接下来可能要执行的一些任务：

- 使用按钮填充文本框。 有关详细信息，请参阅 [演练：使用按钮在文档的文本框中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md)。

- 通过从组合框中选择样式来更改格式设置。 有关详细信息，请参阅 [演练：使用 CheckBox 控件更改文档格式](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)。

## <a name="see-also"></a>另请参阅
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [Office 文档 Windows 窗体控件的限制](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
