---
title: 更改文档格式设置使用 CheckBox 控件
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
ms.openlocfilehash: 24c3cb8d76551bb477f9c13cc56c313519f3b617
ms.sourcegitcommit: 7eb2fb21805d92f085126f3a820ac274f2216b4e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2019
ms.locfileid: "67328729"
---
# <a name="walkthrough-change-document-formatting-using-checkbox-controls"></a>演练：更改文档格式设置使用 CheckBox 控件
  本演练演示如何在 Microsoft Office Word 的文档级自定义项中使用 Windows 窗体控件来更改文本格式。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 本演练阐释了以下任务：

- 在设计时向文档级项目中的文档添加文本和控件。

- 设置文本格式时选择一个选项。

  若要查看已完成的示例，请参阅 Word 控件示例[Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 或 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-the-project"></a>创建项目
 第一步是创建 Word 文档项目。

### <a name="create-a-new-project"></a>创建新项目

1. 使用名称创建一个 Word 文档项目**我的 Word 格式**。 在向导中，选择**创建一个新文档**。

     有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 设计器中打开新的 Word 文档并将添加**我的 Word 格式**投影到**解决方案资源管理器**。

## <a name="add-text-and-controls-to-the-word-document"></a>将文本和控件添加到 Word 文档
 对于本演练中，添加三个复选框和中的某些文本<xref:Microsoft.Office.Tools.Word.Bookmark>到 Word 文档的控件。 对应的复选框将向用户显示的选项，用于设置文本格式。

### <a name="add-three-check-boxes"></a>添加三个复选框

1. 验证该文档已在 Visual Studio 设计器中打开。

2. 从**公共控件**选项卡**工具箱**，将第一个<xref:Microsoft.Office.Tools.Word.Controls.CheckBox>到文档。

3. 在 **“属性”** 窗口中，更改下列属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**applyBoldFont**|
    |**文本**|**加粗**|

4. 按**Enter**移动插入点下面第一个复选框。

5. 将第二个复选框添加到下面的文档`ApplyBoldFont`复选框，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**applyItalicFont**|
    |**文本**|**斜体**|

6. 按**Enter**移动插入点下面第二个复选框。

7. 将第三个复选框添加到下面的文档`ApplyItalicFont`复选框，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**applyUnderlineFont**|
    |**文本**|**用下划线标出**|

### <a name="add-text-and-a-bookmark-control"></a>添加文本和书签控件

1. 移动插入点下方的复选框控件，然后键入以下文本：

    **单击复选框来更改此文本的格式设置。**

2. 从**Word 控件**选项卡**工具箱**，拖动<xref:Microsoft.Office.Tools.Word.Bookmark>到文档。

    **添加书签控件**对话框随即出现。

3. 选择添加到文档的文本，然后单击**确定**。

    一个<xref:Microsoft.Office.Tools.Word.Bookmark>名为控件**Bookmark1**添加到文档中所选文本。

4. 在中**属性**窗口中，更改的值 **（名称）** 属性设置为**fontText。**

   接下来，编写代码以设置文本格式时选中或清除复选框。

## <a name="format-the-text-when-a-check-box-is-checked-or-cleared"></a>设置文本格式时选中或清除复选框
 当用户选择一种格式化选项，更改文档中的文本的格式。

### <a name="change-formatting-when-a-check-box-is-selected"></a>更改时选中复选框格式设置

1. 右键单击`ThisDocument`中**解决方案资源管理器**，然后单击**查看代码**快捷菜单上。

2. 有关C#仅添加到以下常量**ThisDocument**类。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#2](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#2)]

3. 将以下代码添加到<xref:System.Windows.Forms.Control.Click>事件处理程序`applyBoldFont`复选框。

     [!code-vb[Trin_VstcoreProgrammingControlsWord#3](../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb#3)]
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#3](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#3)]

4. 将以下代码添加到<xref:System.Windows.Forms.Control.Click>事件处理程序`applyItalicFont`复选框。

     [!code-vb[Trin_VstcoreProgrammingControlsWord#4](../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb#4)]
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#4](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#4)]

5. 将以下代码添加到<xref:System.Windows.Forms.Control.Click>事件处理程序`applyUnderlineFont`复选框。

     [!code-vb[Trin_VstcoreProgrammingControlsWord#5](../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb#5)]
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#5](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#5)]

6. 在C#，必须将添加到文本框中的事件处理程序<xref:Microsoft.Office.Tools.Word.Document.Startup>事件。 有关如何创建事件处理程序的信息，请参阅[如何：Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#6](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#6)]

## <a name="test-the-application"></a>测试应用程序
 现在可以测试文档以验证文本的格式正确，当您选择或清除复选框。

### <a name="test-your-document"></a>对文档进行测试

1. 按**F5**运行你的项目。

2. 选中或清除复选框。

3. 确认文本已正确设置格式。

## <a name="next-steps"></a>后续步骤
 本演练显示了使用复选框和以编程方式更改文本在 Word 文档格式设置基础的知识。 以下是接下来可能要执行的一些任务：

- 使用按钮填充文本框。 有关详细信息，请参见[演练：在文本框中使用按钮在文档中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md)。

- 使用单选按钮以选择图表样式。 有关详细信息，请参见[演练：更新使用单选按钮在文档结构图](../vsto/walkthrough-updating-a-chart-in-a-document-using-radio-buttons.md)。

## <a name="see-also"></a>请参阅
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [Office 文档上的 Windows 窗体控件的限制](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
