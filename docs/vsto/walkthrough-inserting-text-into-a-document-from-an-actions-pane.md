---
title: 演练：将文本从操作窗格插入到文档中
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840815"
---
# <a name="walkthrough-insert-text-into-a-document-from-an-actions-pane"></a>演练：将文本从操作窗格插入到文档中
  本演练演示如何在 Microsoft Office Word 文档中创建操作窗格。 操作窗格包含两个控件，这些控件收集输入，然后将文本发送到文档。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 本演练演示以下任务：

- 使用操作窗格控件上的 Windows 窗体控件设计接口。

- 当应用程序打开时显示操作窗格。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 或 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-the-project"></a>创建项目
 第一步是创建 Word 文档项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 创建一个名为 **"我的基本操作" 窗格**的 Word 文档项目。 在向导中，选择 " **创建新文档**"。 有关详细信息，请参阅 [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 将在设计器中打开新的 Word 文档，并将 " **我的基本操作" 窗格** 项目添加到 **解决方案资源管理器**。

## <a name="add-text-and-bookmarks-to-the-document"></a>向文档添加文本和书签
 操作窗格会向文档中的书签发送文本。 若要设计文档，请键入一些文本来创建基本窗体。

### <a name="to-add-text-to-your-document"></a>向文档中添加文本

1. 在 Word 文档中键入以下文本：

    **2008年3月21日**

    **名称**

    **Address**

    **这是 Word 中的基本操作窗格的一个示例。**

   您可以通过在 <xref:Microsoft.Office.Tools.Word.Bookmark> Visual Studio 的 " **工具箱** " 中拖动控件或使用 Word 中的 " **书签** " 对话框将控件添加到文档中。

### <a name="to-add-a-bookmark-control-to-your-document"></a>向文档添加书签控件

1. 从 "**工具箱**" 的 " **Word 控件**" 选项卡中，将 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件拖到文档中。

     此时将显示 " **添加书签控件** " 对话框。

2. 选择单词 **名称**，不选择段落标记，然后单击 **"确定"**。

    > [!NOTE]
    > 段落标记应位于书签外。 如果段落标记在文档中不可见，请单击 " **工具** " 菜单，指向 " **Microsoft Office Word 工具** "，然后单击 " **选项**"。 单击 "**查看**" 选项卡，然后在 "**选项**" 对话框的 "**格式标记**" 部分中选中 "**段落标记**" 复选框。

3. 在 "**属性**" 窗口中，将 " **Bookmark1** " 的 "**名称**" 属性更改为 " **showName**"。

4. 选择字 **地址**，而不选择段落标记。

5. 在功能区的 " **插入** " 选项卡上的 " **链接** " 组中，单击 " **书签**"。

6. 在 "**书签**" 对话框中，在 "**书签名称**" 框中键入**ShowAddress** ，然后单击 "**添加**"。

## <a name="add-controls-to-the-actions-pane"></a>向操作窗格添加控件
 若要设计操作窗格界面，请将操作窗格控件添加到项目，然后将 Windows 窗体控件添加到操作窗格控件。

### <a name="to-add-an-actions-pane-control"></a>添加操作窗格控件

1. 在**解决方案资源管理器**中选择 "**我的基本操作" 窗格**项目。

2. 在 **“项目”** 菜单上，单击 **“添加新项”**。

3. 在 " **添加新项** " 对话框中，单击 " **操作窗格控件**"，将控件命名为 " **InsertTextControl"，** 然后单击 " **添加**"。

#### <a name="to-add-windows-form-controls-to-the-actions-pane-control"></a>向操作窗格控件添加 Windows 窗体控件

1. 如果操作窗格控件在设计器中不可见，请双击 " **InsertTextControl**"。

2. 从 "**工具箱**" 的 "**公共控件**" 选项卡中，将 "**标签**" 控件拖动到 "操作" 窗格控件。

3. 将 "标签" 控件的 " **文本** " 属性更改为 " **名称**"。

4. 向操作窗格控件添加 **Textbox** 控件，并更改以下属性。

    |Property|值|
    |--------------|-----------|
    |**名称**|**getName**|
    |**大小**|**130, 20**|

5. 将第二个 " **标签** " 控件添加到 "操作" 窗格控件，并将 " **Text** " 属性更改为 " **Address**"。

6. 将第二个 **Textbox** 控件添加到操作窗格控件，并更改以下属性。

    |Property|值|
    |--------------|-----------|
    |**名称**|**getAddress**|
    |**接受返回**|**True**|
    |**多行**|**True**|
    |**大小**|**130, 40**|

7. 向 "操作" 窗格控件添加 " **按钮** " 控件，并更改以下属性。

    |Property|值|
    |--------------|-----------|
    |**名称**|**Shapes.addtext**|
    |**Text**|插入 |

## <a name="add-code-to-insert-text-into-the-document"></a>添加代码以在文档中插入文本
 在 "操作" 窗格中，编写将文本框中的文本插入 <xref:Microsoft.Office.Tools.Word.Bookmark> 文档中相应控件的代码。 您可以使用 `Globals` 类从 "操作" 窗格上的控件访问文档上的控件。 有关详细信息，请参阅 [对 Office 项目中对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)。

### <a name="to-insert-text-from-the-actions-pane-in-a-bookmark-in-the-document"></a>将操作窗格中的文本插入文档中的书签

1. 将以下代码添加到 <xref:System.Windows.Forms.Control.Click> " **shapes.addtext** " 按钮的事件处理程序。

     [!code-csharp[Trin_VstcoreActionsPaneWord#8](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/InsertTextControl.cs#8)]
     [!code-vb[Trin_VstcoreActionsPaneWord#8](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/InsertTextControl.vb#8)]

2. 在 c # 中，必须为按钮单击添加一个事件处理程序。 可以在调用后将此代码放在 `InsertTextControl` 构造函数中 `InitializeComponent` 。 有关创建事件处理程序的信息，请参阅 [如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreActionsPaneWord#9](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/InsertTextControl.cs#9)]

## <a name="add-code-to-show-the-actions-pane"></a>添加代码以显示操作窗格
 若要显示操作窗格，请将创建的控件添加到控件集合中。

### <a name="to-show-the-actions-pane"></a>显示操作窗格

1. 在类中创建操作窗格控件的新实例 `ThisDocument` 。

     [!code-csharp[Trin_VstcoreActionsPaneWord#10](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#10)]
     [!code-vb[Trin_VstcoreActionsPaneWord#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#10)]

2. 将以下代码添加到的 <xref:Microsoft.Office.Tools.Word.Document.Startup> 事件处理程序中 `ThisDocument` 。

     [!code-csharp[Trin_VstcoreActionsPaneWord#11](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#11)]
     [!code-vb[Trin_VstcoreActionsPaneWord#11](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#11)]

## <a name="test-the-application"></a>测试应用程序
 测试您的文档，以验证在打开文档时操作窗格是否打开，并且在单击该按钮时，将在文本框中键入的文本插入到书签中。

### <a name="to-test-your-document"></a>测试文档

1. 按 **F5** 运行项目。

2. 确认操作窗格可见。

3. 在 "操作" 窗格上的文本框中键入您的姓名和地址，然后单击 " **插入**"。

## <a name="next-steps"></a>后续步骤
 以下是接下来可能要执行的一些任务：

- 在 Excel 中创建操作窗格。 有关详细信息，请参阅 [如何：将操作窗格添加到 Excel 工作簿](/previous-versions/visualstudio/visual-studio-2010/e3zbk0hz(v=vs.100))。

- 将数据绑定到操作窗格上的控件。 有关详细信息，请参阅 [演练：将数据绑定到 Word 操作窗格上的控件](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md)。

## <a name="see-also"></a>请参阅
- [操作窗格概述](../vsto/actions-pane-overview.md)
- [如何：向 Word 文档或 Excel 工作簿添加操作窗格](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [如何：向 Excel 工作簿添加操作窗格](/previous-versions/visualstudio/visual-studio-2010/e3zbk0hz(v=vs.100))
- [如何：管理操作窗格上的控件布局](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [Bookmark 控件](../vsto/bookmark-control.md)
