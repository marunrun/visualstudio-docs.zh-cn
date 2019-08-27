---
title: 在使用按钮在文档中的文本框中显示文本
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- text boxes, displaying text in documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8f3c467abcee8fb4faafd2da06ba261e7f3039fe
ms.sourcegitcommit: 7eb2fb21805d92f085126f3a820ac274f2216b4e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2019
ms.locfileid: "67328754"
---
# <a name="walkthrough-display-text-in-a-text-box-in-a-document-using-a-button"></a>演练：在文本框中使用按钮在文档中显示文本
  本演练演示如何在 Microsoft Office Word 的文档级自定义项中使用按钮和文本框。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 本演练阐释了以下任务：

- 设计时，将控件添加到文档级项目中的 Word 文档。

- 单击按钮时将填充文本框。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word

## <a name="create-the-project"></a>创建项目
 第一步是创建 Word 文档项目。

### <a name="to-create-a-new-project"></a>创建新项目

1. 使用名称创建一个 Word 文档项目**我的 Word 按钮**。 在向导中，选择**创建一个新文档**。

     有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 设计器中打开新的 Word 文档并将添加**我的 Word 按钮**投影到**解决方案资源管理器**。

## <a name="add-controls-to-the-word-document"></a>将控件添加到 Word 文档
 用户界面控件包含一个按钮和一个 Word 文档上的文本框。

### <a name="to-add-a-button-and-a-text-box"></a>添加一个按钮和一个文本框

1. 验证该文档已在 Visual Studio 设计器中打开。

2. 从**公共控件**选项卡**工具箱**，拖动<xref:Microsoft.Office.Tools.Word.Controls.TextBox>到文档。

   > [!NOTE]
   > 在 Word 中，默认情况下控件将按照文本进行删除。 您可以修改的方式控件和形状对象插入上更改默认值**编辑**选项卡**选项**在 Word 中的对话框。

3. 在 **“视图”** 菜单上，单击 **“属性窗口”** 。

4. 查找**TextBox1**中**属性**窗口下拉列表框，然后**名称**属性的文本设置为**displayText**。

5. 拖动**按钮**控制对文档和更改以下属性。

   |属性|值|
   |--------------|-----------|
   |**名称**|**insertText**|
   |**文本**|**插入文本**|

   现在，你可以编写将在单击该按钮时运行的代码。

## <a name="populate-the-text-box-when-the-button-is-clicked"></a>单击该按钮填充文本框
 每次用户单击按钮， **Hello World ！** 添加到文本框中。

### <a name="to-write-to-the-text-box-when-the-button-is-clicked"></a>在单击按钮时写入文本框

1. 在中**解决方案资源管理器**，右键单击**ThisDocument**，然后单击**查看代码**快捷菜单上。

2. 将下列代码添加到按钮的 <xref:System.Windows.Forms.Control.Click> 事件处理程序。

     [!code-vb[Trin_VstcoreProgrammingControlsWord#7](../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb#7)]
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#7](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#7)]

3. 在 C# 中，必须向 <xref:Microsoft.Office.Tools.Word.Document.Startup> 事件添加按钮的事件处理程序。 有关创建事件处理程序的信息，请参阅[如何：Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#8](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#8)]

## <a name="test-the-application"></a>测试应用程序
 现在可以测试文档，以确保消息**Hello World ！** 单击此按钮时将其显示在文本框中。

### <a name="to-test-your-document"></a>测试文档

1. 按**F5**运行你的项目。

2. 单击按钮。

3. 确认**Hello World ！** 显示在文本框中。

## <a name="next-steps"></a>后续步骤
 本演练演示在 Word 文档中使用按钮和文本框的基础知识。 以下是接下来可能要执行的一些任务：

- 使用组合框来更改格式设置。 有关详细信息，请参见[演练：使用 CheckBox 控件更改文档格式设置](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)。

- 使用单选按钮以选择图表样式。 有关详细信息，请参见[演练：更新使用单选按钮在文档结构图](../vsto/walkthrough-updating-a-chart-in-a-document-using-radio-buttons.md)。

## <a name="see-also"></a>请参阅
- [Windows 窗体控件在 Office 文档概述](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [如何：向 Office 文档添加 Windows 窗体控件](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
