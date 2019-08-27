---
title: 演练：创建书签的快捷菜单
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- context menus, Word
- Bookmark control, events
- shortcut menus, Word
- menus, creating in Office applications
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9b4b412d2e9456142c1be1af388e2803634d15c0
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438542"
---
# <a name="walkthrough-create-shortcut-menus-for-bookmarks"></a>演练：创建书签的快捷菜单
  本演练演示如何创建快捷方式菜单<xref:Microsoft.Office.Tools.Word.Bookmark>Word 的文档级自定义项中的控件。 后在用户右键单击一个书签中的文本，快捷菜单会显示，并将用于设置文本格式的用户选项。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 本演练阐释了以下任务：

- [创建项目](#BKMK_CreateProject)。

- [向文档添加文本和书签](#BKMK_addtextandbookmarks)。

- [将命令添加到快捷菜单](#BKMK_AddCmndsShortMenu)。

- [在书签中的文本格式](#BKMK_formattextbkmk)。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 或 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]

## <a name="BKMK_CreateProject"></a> 创建项目
 第一步是在 Visual Studio 中创建一个 Word 文档项目。

### <a name="to-create-a-new-project"></a>创建新项目

- 创建具有名称的 Word 文档项目**我的书签快捷方式菜单**。 在向导中，选择**创建一个新文档**。 有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 设计器中打开新的 Word 文档并将添加**我的书签快捷方式菜单**投影到**解决方案资源管理器**。

## <a name="BKMK_addtextandbookmarks"></a> 向文档添加文本和书签
 向文档添加一些文本，然后添加两个重叠书签。

### <a name="to-add-text-to-your-document"></a>若要将文本添加到你的文档

- 在文档中显示在你的项目设计器中，键入以下文本。

     **这是创建一个快捷菜单，右键单击一个书签中的文本时的示例。**

### <a name="to-add-a-bookmark-control-to-your-document"></a>若要向文档添加书签控件

1. 在中**工具箱**，从**Word 控件**选项卡上，拖动<xref:Microsoft.Office.Tools.Word.Bookmark>到你的文档的控件。

    **添加书签控件**对话框随即出现。

2. 选择"创建快捷菜单，右键单击文本时"的单词，然后单击**确定**。

    `bookmark1` 将添加到文档。

3. 添加另一个<xref:Microsoft.Office.Tools.Word.Bookmark>控制对单词"右键单击一个书签中的文本"。

    `bookmark2` 将添加到文档。

   > [!NOTE]
   > "右键单击文本"会同时出现在单词`bookmark1`和`bookmark2`。

   当在设计时向文档添加书签时<xref:Microsoft.Office.Tools.Word.Bookmark>创建控件。 您可以对该书签的多个事件进行编程。 可以在编写代码<xref:Microsoft.Office.Tools.Word.Bookmark.BeforeRightClick>事件的书签，以便当用户右键单击该书签中的文本将出现快捷菜单。

## <a name="BKMK_AddCmndsShortMenu"></a> 将命令添加到快捷菜单
 向右键单击该文档时，将显示的快捷菜单添加按钮。

### <a name="to-add-commands-to-a-shortcut-menu"></a>若要将命令添加到快捷菜单

1. 添加**功能区 XML**到项目的项。 有关详细信息，请参阅[如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)。

2. 在中**解决方案资源管理器**，选择**ThisDocument.cs**或**ThisDocument.vb**。

3. 在菜单栏上，选择“视图” > “代码”。

     **ThisDocument**类文件随即在代码编辑器中打开。

4. 将以下代码添加到**ThisDocument**类。 此代码将重写 CreateRibbonExtensibilityObject 方法并返回到 Office 应用程序的功能区 XML 类。

     [!code-csharp[Trin_Word_Document_Menus#1](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#1)]
     [!code-vb[Trin_Word_Document_Menus#1](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb#1)]

5. 在“解决方案资源管理器” 中，选择功能区 XML 文件。 默认情况下，功能区 XML 文件命名为 Ribbon1.xml。

6. 在菜单栏上，选择“视图” > “代码”。

     功能区 XML 文件随即在代码编辑器中打开。

7. 在代码编辑器中，将以下代码替换为功能区 XML 文件的内容。

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <customUI xmlns="http://schemas.microsoft.com/office/2009/07/customui" onLoad="Ribbon_Load">
      <contextMenus>
        <contextMenu idMso="ContextMenuText">
          <button id="BoldButton" label="Bold" onAction="ButtonClick"
               getVisible="GetVisible" />
          <button id="ItalicButton" label="Italic" onAction="ButtonClick"
              getVisible="GetVisible"/>
        </contextMenu>
      </contextMenus>
    </customUI>
    ```

     此代码添加到快捷菜单，右键单击该文档时，将显示两个按钮。

8. 在中**解决方案资源管理器**，右键单击`ThisDocument`，然后单击**查看代码**。

9. 声明以下变量，并在类级别的书签变量。

     [!code-csharp[Trin_Word_Document_Menus#2](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#2)]
     [!code-vb[Trin_Word_Document_Menus#2](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb#2)]

10. 在中**解决方案资源管理器**，选择功能区代码文件。 默认情况下，功能区代码文件命名为**Ribbon1.cs**或**Ribbon1.vb**。

11. 在菜单栏上，选择“视图” > “代码”。

     功能区代码文件将在代码编辑器中打开。

12. 在功能区代码文件中，添加以下方法。 这是已添加到文档的快捷菜单的两个按钮的回调方法。 此方法确定是否在快捷菜单中显示这些按钮。 粗体和斜体按钮显示仅当您右键单击该书签中的文本。

     [!code-csharp[Trin_Word_Document_Menus#5](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/ribbon1.cs#5)]
     [!code-vb[Trin_Word_Document_Menus#5](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/ribbon1.vb#5)]

## <a name="BKMK_formattextbkmk"></a> 在书签中的文本格式

### <a name="to-format-the-text-in-the-bookmark"></a>若要在书签中的文本格式

1. 在功能区代码文件中添加`ButtonClick`事件处理程序以将格式应用于该书签。

     [!code-csharp[Trin_Word_Document_Menus#6](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/ribbon1.cs#6)]
     [!code-vb[Trin_Word_Document_Menus#6](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/ribbon1.vb#6)]

2. **解决方案资源管理器**，选择**ThisDocument.cs**或**ThisDocument.vb**。

3. 在菜单栏上，选择“视图” > “代码”。

     **ThisDocument**类文件随即在代码编辑器中打开。

4. 将以下代码添加到**ThisDocument**类。

     [!code-csharp[Trin_Word_Document_Menus#3](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#3)]
     [!code-vb[Trin_Word_Document_Menus#3](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb#3)]

    > [!NOTE]
    > 必须编写代码以处理书签与发生重叠的情况。 如果不这样做，默认情况下，代码将调用所选内容中的所有书签。

5. 在 C# 中，必须添加到的书签控件的事件处理程序<xref:Microsoft.Office.Tools.Word.Document.Startup>事件。 有关创建事件处理程序的信息，请参阅[如何：Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_Word_Document_Menus#4](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#4)]

## <a name="test-the-application"></a>测试应用程序
 测试文档，以验证，粗体和斜体菜单项显示在快捷菜单中右键单击书签中的文本和文本的格式正确。

### <a name="to-test-your-document"></a>测试文档

1. 按**F5**运行你的项目。

2. 中的第一个书签，右键单击，然后单击**加粗**。

3. 验证中的文本的所有`bookmark1`设置为粗体。

4. 右键单击的文本个重叠书签，然后单击**斜体**。

5. 验证所有中的文本`bookmark2`为斜体，并仅在文本的一部分`bookmark1`重叠`bookmark2`为斜体。

## <a name="next-steps"></a>后续步骤
 以下是接下来可能要执行的一些任务：

- 编写代码以响应在 Excel 中的主机控件的事件。 有关详细信息，请参见[演练：针对 NamedRange 控件的事件进行编程](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)。

- 使用复选框来更改格式设置在书签中。 有关详细信息，请参见[演练：使用 CheckBox 控件更改文档格式设置](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)。

## <a name="see-also"></a>请参阅
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [Office UI 自定义](../vsto/office-ui-customization.md)
- [通过使用扩展的对象自动化 Word](../vsto/automating-word-by-using-extended-objects.md)
- [Bookmark 控件](../vsto/bookmark-control.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
