---
title: 使用 CheckBox 控件更改文档格式
description: 了解如何在 Microsoft Word 的文档级自定义项中使用 Windows 窗体控件来更改文本格式。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word documents, changing formatting using controls
- documents [Office development in Visual Studio], formatting
- check boxes, Word documents
- documents [Office development in Visual Studio], check box controls
- controls [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 931e9554a10e0e1525d9ee4a10505633b211610b
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97527253"
---
# <a name="walkthrough-change-document-formatting-using-checkbox-controls"></a>演练：使用 CheckBox 控件更改文档格式
  本演练演示如何在 Microsoft Office Word 的文档级自定义项中使用 Windows 窗体控件来更改文本格式。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 本演练演示以下任务：

- 在设计时向文档级项目中的文档添加文本和控件。

- 选择选项时设置文本格式。

  若要查看已完成示例的结果，请参阅 [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)中的 Word 控件示例。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 或 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-the-project"></a>创建项目
 第一步是创建 Word 文档项目。

### <a name="create-a-new-project"></a>创建新项目

1. 创建一个名为 **My Word 格式** 的 word 文档项目。 在向导中，选择 " **创建新文档**"。

     有关详细信息，请参阅 [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 将在设计器中打开新的 Word 文档，并将 **My Word 格式** 项目添加到 **解决方案资源管理器**。

## <a name="add-text-and-controls-to-the-word-document"></a>向 Word 文档添加文本和控件
 对于本演练，请将控件中的三个复选框和一些文本添加 <xref:Microsoft.Office.Tools.Word.Bookmark> 到 Word 文档中。 复选框将向用户显示用于设置文本格式的选项。

### <a name="add-three-check-boxes"></a>添加三个复选框

1. 验证该文档已在 Visual Studio 设计器中打开。

2. 从 "**工具箱**" 的 "**公共控件**" 选项卡中，将第一个 <xref:Microsoft.Office.Tools.Word.Controls.CheckBox> 控件拖动到文档。

3. 在 **“属性”** 窗口中，更改下列属性。

    |properties|值|
    |--------------|-----------|
    |**名称**|**applyBoldFont**|
    |**文本**|**加粗**|

4. 按 **enter** 将插入点移动到第一个复选框下。

5. 将第二个复选框添加到该复选框下的文档中 `ApplyBoldFont` ，并更改以下属性。

    |properties|值|
    |--------------|-----------|
    |**名称**|**applyItalicFont**|
    |**文本**|**斜体**|

6. 按 **enter** 将插入点移动到第二个复选框下。

7. 将第三个复选框添加到该复选框下的文档中 `ApplyItalicFont` ，并更改以下属性。

    |properties|值|
    |--------------|-----------|
    |**名称**|**applyUnderlineFont**|
    |**文本**|**下划线**|

### <a name="add-text-and-a-bookmark-control"></a>添加文本和书签控件

1. 将插入点移到复选框控件的下方，然后键入以下文本：

    **单击复选框以更改此文本的格式设置。**

2. 从 "**工具箱**" 的 " **Word 控件**" 选项卡中，将 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件拖动到文档。

    此时将显示 " **添加书签控件** " 对话框。

3. 选择已添加到文档中的文本，然后单击 **"确定"**。

    <xref:Microsoft.Office.Tools.Word.Bookmark>名为 **Bookmark1** 的控件将添加到文档中的选定文本。

4. 在 " **属性** " 窗口中，将 " **(名称)** " 属性的值更改为 " **fontText"。**

   接下来，在选中或清除复选框时编写代码以设置文本格式。

## <a name="format-the-text-when-a-check-box-is-checked-or-cleared"></a>选中或清除复选框时设置文本格式
 当用户选择格式设置选项时，请更改文档中文本的格式。

### <a name="change-formatting-when-a-check-box-is-selected"></a>选中复选框时更改格式设置

1. 右键单击 `ThisDocument` **解决方案资源管理器**，然后单击快捷菜单上的 " **查看代码** "。

2. 仅适用于 c #，将以下常量添加到 **ThisDocument** 类。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#2](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#2)]

3. 将以下代码添加到 <xref:System.Windows.Forms.Control.Click> 该复选框的事件处理程序中 `applyBoldFont` 。

     [!code-vb[Trin_VstcoreProgrammingControlsWord#3](../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb#3)]
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#3](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#3)]

4. 将以下代码添加到 <xref:System.Windows.Forms.Control.Click> 该复选框的事件处理程序中 `applyItalicFont` 。

     [!code-vb[Trin_VstcoreProgrammingControlsWord#4](../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb#4)]
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#4](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#4)]

5. 将以下代码添加到 <xref:System.Windows.Forms.Control.Click> 该复选框的事件处理程序中 `applyUnderlineFont` 。

     [!code-vb[Trin_VstcoreProgrammingControlsWord#5](../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb#5)]
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#5](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#5)]

6. 在 c # 中，必须向事件添加文本框的事件处理程序 <xref:Microsoft.Office.Tools.Word.Document.Startup> 。 有关如何创建事件处理程序的信息，请参阅 [如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#6](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#6)]

## <a name="test-the-application"></a>测试应用程序
 现在可以对文档进行测试，以便在选中或清除复选框时验证文本格式是否正确。

### <a name="test-your-document"></a>测试文档

1. 按 **F5** 运行项目。

2. 选中或清除复选框。

3. 确认文本格式正确。

## <a name="next-steps"></a>后续步骤
 此演练演示了使用复选框和以编程方式更改 Word 文档中的文本格式的基本知识。 以下是接下来可能要执行的一些任务：

- 使用按钮填充文本框。 有关详细信息，请参阅 [演练：使用按钮在文档的文本框中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md)。

- 使用单选按钮以选择图表样式。 有关详细信息，请参阅 [演练：使用单选按钮更新文档中的图表](../vsto/walkthrough-updating-a-chart-in-a-document-using-radio-buttons.md)。

## <a name="see-also"></a>另请参阅
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [Office 文档 Windows 窗体控件的限制](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
