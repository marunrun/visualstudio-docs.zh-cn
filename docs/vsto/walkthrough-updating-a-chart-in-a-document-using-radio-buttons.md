---
title: 演练：更新的图表中使用单选按钮的文档
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62981044"
---
# <a name="walkthrough-update-a-chart-in-a-document-using-radio-buttons"></a>演练：更新的图表中使用单选按钮的文档
  此演练演示如何使用 Microsoft Office Word 文档级自定义中的单选按钮，为用户提供在文档中选择图表样式的选项。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 本演练阐释了以下任务：

- 在文档级项目中，在设计时向文档中添加图表。

- 通过将单选按钮添加到用户控件来对它们进行分组。

- 在选择了某个选项时更改图表样式。

  若要查看已完成的示例，请参阅 Word 控件示例[Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 或 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-the-project"></a>创建项目
 第一步是创建 Word 文档项目。

### <a name="to-create-a-new-project"></a>创建新项目

1. 使用名称创建一个 Word 文档项目**我的图表选项**。 在向导中，选择**创建一个新文档**。 有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 设计器中打开新的 Word 文档并将添加**我的图表选项**投影到**解决方案资源管理器**。

## <a name="add-a-chart-to-the-document"></a>将图表添加到文档

### <a name="to-add-a-chart"></a>添加图表

1. 在托管在 Visual Studio 设计器中，在功能区上的 Word 文档中，单击**插入**选项卡。

2. 在中**文本**组中，单击**插入对象**下拉列表按钮，然后单击**对象**。

     **对象**对话框随即打开。

3. 在中**对象类型**上列出**创建新**选项卡上，选择**Microsoft Graph 图表**，然后单击**确定**。

     图表添加到插入点处的文档和**数据表**窗口中会显示一些默认数据。

4. 关闭**数据表**窗口以接受在图表中的默认值，然后单击要将焦点从图表移的文档中。

5. 右键单击图表，然后依次**格式对象**。

6. 上**布局**选项卡**设置对象格式**对话框中，选择**正方形**然后单击**确定**。

## <a name="add-a-user-control-to-the-project"></a>将用户控件添加到项目中
 文档上的单选按钮默认情况下不互相排斥。 通过将这些按钮添加到用户控件中，然后编写代码来控制选择，可使这些按钮正常工作。

### <a name="to-add-a-user-control"></a>要添加用户控件

1. 选择**我的图表选项**项目中**解决方案资源管理器**。

2. 在 **“项目”** 菜单上，单击 **“添加新项”**。

3. 在**添加新项**对话框中，单击**用户控件**，将控件**ChartOptions，** 然后单击**添加**。

### <a name="to-add-windows-form-controls-to-the-user-control"></a>向用户控件添加 Windows 窗体控件

1. 如果用户控件不可见的设计器中，双击**ChartOptions**中**解决方案资源管理器**。

2. 从**公共控件**选项卡**工具箱**，将第一个**单选按钮**控制转移到该用户控件，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**columnChart**|
    |**文本**|**柱形图**|

3. 添加另一个**单选按钮**向用户控件，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**barChart**|
    |**文本**|**条形图**|

4. 添加第三个**单选按钮**向用户控件，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**lineChart**|
    |**文本**|**折线图**|

5. 添加第四个**单选按钮**向用户控件，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**areaBlockChart**|
    |**文本**|**面积图**|

## <a name="add-references"></a>添加引用
 若要从文档上的用户控件访问图表，必须具有对引用`Microsoft.Office.Interop.Graph`在项目中的程序集。

### <a name="to-add-a-reference-to-the-microsoftofficeinteropgraph-assembly"></a>添加对 Microsoft.Office.Interop.Graph 程序集的引用

1. 在“项目”菜单上，单击“添加引用”。

     此时会显示“添加引用”对话框。

2. 上 **.NET**选项卡上，选择**Microsoft.Office.Interop.Graph**然后单击**确定**。 选择该程序集的 14.0.0.0 版。

## <a name="change-the-chart-style-when-a-radio-button-is-selected"></a>单选按钮处于选中状态时更改图表样式
 若要使这些按钮正常工作，请创建用户控件的公共事件，添加属性以设置选择类型，并为每个单选按钮的 `CheckedChanged` 事件创建过程。

### <a name="to-create-an-event-and-property-on-a-user-control"></a>创建用户控件的事件和属性

1. 在中**解决方案资源管理器**，右键单击用户控件，然后单击**查看代码**。

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

5. 在 C# 中，必须为单选按钮添加事件处理程序。 可以将此代码添加到 `ChartOptions` 构造函数中 `InitializeComponent` 调用的下面。 有关创建事件处理程序的信息，请参阅[如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#14](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#14)]

## <a name="add-the-user-control-to-the-document"></a>将用户控件添加到文档
 生成解决方案时，新的用户控件自动添加到**工具箱**。 然后，可以将控件从**工具箱**到你的文档。

### <a name="to-add-the-user-control-your-document"></a>向文档添加用户控件

1. 在 **“生成”** 菜单上，单击 **“生成解决方案”**。

     **ChartOptions**用户控件添加到**工具箱**。

2. 在中**解决方案资源管理器**，右键单击**ThisDocument.vb**或**ThisDocument.cs**，然后单击**视图设计器**。

3. 拖动`ChartOptions`控件从**工具箱**到文档。

     在中**属性**窗口中，您只是该控件添加到文档的名称`ChartOptions1`。

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

1. 按**F5**运行你的项目。

2. 选择不同的单选按钮。

3. 确认图表样式随所选选项发生了相应的更改。

## <a name="next-steps"></a>后续步骤
 以下是接下来可能要执行的一些任务：

- 使用按钮填充文本框。 有关详细信息，请参见[演练：在文本框中使用按钮在文档中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md)。

- 通过从组合框中选择样式来更改格式设置。 有关详细信息，请参见[演练：使用 CheckBox 控件更改文档格式设置](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)。

## <a name="see-also"></a>请参阅
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [Office 文档上的 Windows 窗体控件的限制](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
