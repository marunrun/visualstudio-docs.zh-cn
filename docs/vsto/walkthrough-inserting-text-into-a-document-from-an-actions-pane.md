---
title: 演练：从操作窗格的文档中插入文本
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- smart documents [Office development in Visual Studio], creating in Word
- smart documents [Office development in Visual Studio], adding controls
- actions panes [Office development in Visual Studio], creating in Word
- actions panes [Office development in Visual Studio], adding controls
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 61e71f31ce887c7e1ea9ec57b0aa3f24a45be364
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63414285"
---
# <a name="walkthrough-insert-text-into-a-document-from-an-actions-pane"></a>演练：从操作窗格的文档中插入文本
  本演练演示如何在 Microsoft Office Word 文档中创建操作窗格。 操作窗格包含两个控件收集输入，然后将文本发送到该文档。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 本演练阐释了以下任务：

- 通过使用 Windows 窗体控件在操作窗格控件设计一个接口。

- 当应用程序打开时显示操作窗格。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 或 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-the-project"></a>创建项目
 第一步是创建 Word 文档项目。

### <a name="to-create-a-new-project"></a>创建新项目

1. 使用名称创建一个 Word 文档项目**我的基本操作窗格**。 在向导中，选择**创建一个新文档**。 有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 设计器中打开新的 Word 文档并将添加**我的基本操作窗格**投影到**解决方案资源管理器**。

## <a name="add-text-and-bookmarks-to-the-document"></a>向文档添加文本和书签
 操作窗格会将文本发送到文档中的书签。 若要设计文档，键入一些文本，以创建一个基本窗体。

### <a name="to-add-text-to-your-document"></a>若要将文本添加到你的文档

1. 插入到 Word 文档中键入以下文本：

    **2008 年 3 月 21日日**

    **名称**

    **地址**

    **这是一个基本的操作窗格在 Word 中的示例。**

   可以添加<xref:Microsoft.Office.Tools.Word.Bookmark>到你的文档通过将其从控件**工具箱**在 Visual Studio 中或通过使用**书签**在 Word 中的对话框。

### <a name="to-add-a-bookmark-control-to-your-document"></a>若要向文档添加书签控件

1. 从**Word 控件**选项卡**工具箱**，拖动<xref:Microsoft.Office.Tools.Word.Bookmark>到你的文档的控件。

     **添加书签控件**对话框随即出现。

2. 选择该单词**名称**，而不选择段落标记，然后单击**确定**。

    > [!NOTE]
    > 段落标记应为外部书签。 如果段落标记是不可见的文档中，单击**工具**菜单，依次指向**Microsoft Office Word 工具**，然后单击**选项**。 单击**视图**选项卡，然后选择**段落标记**中的复选框**格式设置标记**一部分**选项**对话框。

3. 在中**属性**窗口中，更改**名称**属性**Bookmark1**到**showName**。

4. 选择该单词**地址**，而不选择段落标记。

5. 上**插入**功能区选项卡，在**链接**组中，单击**书签**。

6. 在中**书签**对话框中，键入**showAddress**中**书签名称**框，然后单击**添加**。

## <a name="add-controls-to-the-actions-pane"></a>将控件添加到操作窗格
 若要设计操作窗格界面，将操作窗格控件添加到项目，然后将 Windows 窗体控件添加到操作窗格控件。

### <a name="to-add-an-actions-pane-control"></a>若要添加操作窗格控件

1. 选择**我的基本操作窗格**项目中**解决方案资源管理器**。

2. 在 **“项目”** 菜单上，单击 **“添加新项”** 。

3. 在中**添加新项**对话框中，单击**操作窗格控件**，将控件**InsertTextControl，** 然后单击**添加**。

#### <a name="to-add-windows-form-controls-to-the-actions-pane-control"></a>若要将 Windows 窗体控件添加到操作窗格控件

1. 如果操作窗格控件不可见的设计器中，双击**InsertTextControl**。

2. 从**公共控件**选项卡**工具箱**，将**标签**到操作窗格控件的控件。

3. 更改**文本**该标签控件的属性**名称**。

4. 添加**文本框中**控制对操作窗格控件，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**getName**|
    |**Size**|**130, 20**|

5. 添加另一个**标签**控制对操作窗格控件，并更改**文本**属性设置为**地址**。

6. 添加另一个**文本框中**控制对操作窗格控件，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**getAddress**|
    |**接受返回**|**True**|
    |**多行**|**True**|
    |**Size**|**130, 40**|

7. 添加**按钮**控制对操作窗格控件，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**addText**|
    |**文本**|**插入**|

## <a name="add-code-to-insert-text-into-the-document"></a>添加代码以将文本插入到文档
 在操作窗格中，编写将文本从文本框插入到相应的代码<xref:Microsoft.Office.Tools.Word.Bookmark>文档中的控件。 可以使用`Globals`类来访问文档上的控件从操作窗格上的控件。 有关详细信息，请参阅[对 Office 项目中的对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)。

### <a name="to-insert-text-from-the-actions-pane-in-a-bookmark-in-the-document"></a>若要在文档中的书签的操作窗格中插入文本

1. 将以下代码添加到<xref:System.Windows.Forms.Control.Click>事件处理程序**addText**按钮。

     [!code-csharp[Trin_VstcoreActionsPaneWord#8](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/InsertTextControl.cs#8)]
     [!code-vb[Trin_VstcoreActionsPaneWord#8](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/InsertTextControl.vb#8)]

2. 在 C# 中，必须添加为按钮单击事件处理程序。 您可以将此代码放置在`InsertTextControl`构造函数调用的后面`InitializeComponent`。 有关创建事件处理程序的信息，请参阅[如何：Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreActionsPaneWord#9](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/InsertTextControl.cs#9)]

## <a name="add-code-to-show-the-actions-pane"></a>添加代码以显示操作窗格
 若要显示操作窗格，添加到控件集合您创建的控件。

### <a name="to-show-the-actions-pane"></a>若要显示操作窗格

1. 创建操作窗格控件中的新实例`ThisDocument`类。

     [!code-csharp[Trin_VstcoreActionsPaneWord#10](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#10)]
     [!code-vb[Trin_VstcoreActionsPaneWord#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#10)]

2. 将以下代码添加到<xref:Microsoft.Office.Tools.Word.Document.Startup>事件处理程序`ThisDocument`。

     [!code-csharp[Trin_VstcoreActionsPaneWord#11](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#11)]
     [!code-vb[Trin_VstcoreActionsPaneWord#11](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#11)]

## <a name="test-the-application"></a>测试应用程序
 若要验证操作窗格打开时打开该文档并在文本框中键入文本插入书签时单击该按钮对文档进行测试。

### <a name="to-test-your-document"></a>测试文档

1. 按**F5**运行你的项目。

2. 确认操作窗格可见。

3. 在操作窗格上的文本框中键入名称和地址，然后单击**插入**。

## <a name="next-steps"></a>后续步骤
 以下是接下来可能要执行的一些任务：

- 在 Excel 中创建操作窗格。 有关详细信息，请参阅[如何：将操作窗格添加到 Excel 工作簿](/previous-versions/visualstudio/visual-studio-2010/e3zbk0hz(v=vs.100))。

- 将数据绑定到操作窗格上的控件。 有关详细信息，请参见[演练：将数据绑定到 Word 操作窗格上的控件](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md)。

## <a name="see-also"></a>请参阅
- [操作窗格概述](../vsto/actions-pane-overview.md)
- [如何：将操作窗格添加到 Word 文档或 Excel 工作簿](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [如何：将操作窗格添加到 Excel 工作簿](/previous-versions/visualstudio/visual-studio-2010/e3zbk0hz(v=vs.100))
- [如何：管理操作窗格上的控件布局](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [Bookmark 控件](../vsto/bookmark-control.md)
