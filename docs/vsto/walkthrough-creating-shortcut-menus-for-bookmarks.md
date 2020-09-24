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
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "91146901"
---
# <a name="walkthrough-create-shortcut-menus-for-bookmarks"></a>演练：创建书签的快捷菜单
  本演练演示如何 <xref:Microsoft.Office.Tools.Word.Bookmark> 在 Word 的文档级自定义项中创建控件的快捷菜单。 当用户右键单击书签中的文本时，将出现一个快捷菜单，并为用户提供用于设置文本格式的选项。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 本演练演示以下任务：

- [创建项目](#BKMK_CreateProject)。

- [向文档添加文本和书签](#BKMK_addtextandbookmarks)。

- [将命令添加到快捷菜单](#BKMK_AddCmndsShortMenu)。

- [设置书签中的文本格式](#BKMK_formattextbkmk)。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 或 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]

## <a name="create-the-project"></a><a name="BKMK_CreateProject"></a> 创建项目
 第一步是在 Visual Studio 中创建 Word 文档项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

- 创建一个名为 **"我的书签" 快捷菜单**的 Word 文档项目。 在向导中，选择 " **创建新文档**"。 有关详细信息，请参阅 [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 将在设计器中打开新的 Word 文档，并将 " **我的书签" 快捷菜单** 项目添加到 **解决方案资源管理器**。

## <a name="add-text-and-bookmarks-to-the-document"></a><a name="BKMK_addtextandbookmarks"></a> 向文档添加文本和书签
 向文档添加一些文本，然后添加两个重叠书签。

### <a name="to-add-text-to-your-document"></a>向文档中添加文本

- 在项目设计器中显示的文档中，键入以下文本。

     **这是在右键单击书签中的文本时创建快捷菜单的示例。**

### <a name="to-add-a-bookmark-control-to-your-document"></a>向文档添加书签控件

1. 在 " **工具箱**" 的 " **Word 控件** " 选项卡中，将 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件拖到文档中。

    此时将显示 " **添加书签控件** " 对话框。

2. 右键单击文本 "，然后单击" **确定**"，即可选择" 创建快捷菜单 "字样。

    `bookmark1` 添加到文档中。

3. 将另一个 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件添加到单词 "右键单击书签中的文本"。

    `bookmark2` 添加到文档中。

   > [!NOTE]
   > 和中都有 "右键单击文本" 字样 `bookmark1` `bookmark2` 。

   在设计时向文档添加书签时，将 <xref:Microsoft.Office.Tools.Word.Bookmark> 创建一个控件。 您可以对书签的多个事件进行编程。 您可以在书签的事件中编写代码 <xref:Microsoft.Office.Tools.Word.Bookmark.BeforeRightClick> ，以便在用户右键单击书签中的文本时，将出现一个快捷菜单。

## <a name="add-commands-to-a-shortcut-menu"></a><a name="BKMK_AddCmndsShortMenu"></a> 向快捷菜单中添加命令
 将按钮添加到右键单击文档时显示的快捷菜单。

### <a name="to-add-commands-to-a-shortcut-menu"></a>向快捷菜单中添加命令

1. 向项目添加 **功能区 XML** 项。 有关详细信息，请参阅 [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)。

2. 在 **解决方案资源管理器**中，选择 " **ThisDocument.cs** " 或 " **ThisDocument**"。

3. 在菜单栏上，选择 "**查看**  >  **代码**"。

     **ThisDocument**类文件将在代码编辑器中打开。

4. 将以下代码添加到 **ThisDocument** 类。 此代码重写 CreateRibbonExtensibilityObject 方法，并将功能区 XML 类返回到 Office 应用程序。

     [!code-csharp[Trin_Word_Document_Menus#1](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#1)]
     [!code-vb[Trin_Word_Document_Menus#1](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb#1)]

5. 在“解决方案资源管理器” **** 中，选择功能区 XML 文件。 默认情况下，功能区 XML 文件命名为 Ribbon1.xml。

6. 在菜单栏上，选择 "**查看**  >  **代码**"。

     功能区 XML 文件随即在代码编辑器中打开。

7. 在代码编辑器中，用以下代码替换功能区 XML 文件的内容。

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

     此代码将两个按钮添加到快捷菜单中，当您右键单击该文档时，将显示该菜单。

8. 在 **解决方案资源管理器**中，右键单击 `ThisDocument` ，然后单击 " **查看代码**"。

9. 在类级别声明以下变量和书签变量。

     [!code-csharp[Trin_Word_Document_Menus#2](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#2)]
     [!code-vb[Trin_Word_Document_Menus#2](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb#2)]

10. 在 **解决方案资源管理器**中，选择功能区代码文件。 默认情况下，功能区代码文件命名为 **Ribbon1.cs** 或 **ribbon1.mfcribbon-ms**。

11. 在菜单栏上，选择 "**查看**  >  **代码**"。

     功能区代码文件将在代码编辑器中打开。

12. 在功能区代码文件中，添加以下方法。 对于已添加到文档快捷菜单的两个按钮，这是一个回调方法。 此方法确定这些按钮是否显示在快捷菜单中。 只有当您右键单击书签中的文本时，才会显示粗体和斜体按钮。

     [!code-csharp[Trin_Word_Document_Menus#5](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/ribbon1.cs#5)]
     [!code-vb[Trin_Word_Document_Menus#5](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/ribbon1.vb#5)]

## <a name="format-the-text-in-the-bookmark"></a><a name="BKMK_formattextbkmk"></a> 设置书签中的文本格式

### <a name="to-format-the-text-in-the-bookmark"></a>设置书签中的文本格式

1. 在功能区代码文件中，添加一个 `ButtonClick` 事件处理程序，以将格式设置应用于书签。

     [!code-csharp[Trin_Word_Document_Menus#6](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/ribbon1.cs#6)]
     [!code-vb[Trin_Word_Document_Menus#6](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/ribbon1.vb#6)]

2. **解决方案资源管理器**中，选择 " **ThisDocument.cs** " 或 " **ThisDocument**"。

3. 在菜单栏上，选择 "**查看**  >  **代码**"。

     **ThisDocument**类文件将在代码编辑器中打开。

4. 将以下代码添加到 **ThisDocument** 类。

     [!code-csharp[Trin_Word_Document_Menus#3](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#3)]
     [!code-vb[Trin_Word_Document_Menus#3](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb#3)]

    > [!NOTE]
    > 您必须编写代码来处理书签重叠的情况。 如果不这样做，则默认情况下，将对选定内容中的所有书签调用代码。

5. 在 c # 中，必须向事件添加书签控件的事件处理程序 <xref:Microsoft.Office.Tools.Word.Document.Startup> 。 有关创建事件处理程序的信息，请参阅 [如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_Word_Document_Menus#4](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#4)]

## <a name="test-the-application"></a>测试应用程序
 测试您的文档，以验证当您右键单击书签中的文本时，快捷菜单中的 "粗体" 和 "斜体" 菜单项将显示，并且该文本格式正确。

### <a name="to-test-your-document"></a>测试文档

1. 按 **F5** 运行项目。

2. 右键单击第一个书签，然后单击 " **加粗**"。

3. 验证中的所有文本 `bookmark1` 是否格式化为粗体。

4. 右键单击书签重叠的文本，然后单击 " **斜体**"。

5. 验证中的所有文本 `bookmark2` 都是斜体，并且只有其中的部分文本 `bookmark1` `bookmark2` 是斜体。

## <a name="next-steps"></a>后续步骤
 以下是接下来可能要执行的一些任务：

- 编写代码以响应 Excel 中的主机控件事件。 有关详细信息，请参阅 [演练：针对 NamedRange 控件的事件进行编程](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)。

- 使用复选框可以更改书签中的格式设置。 有关详细信息，请参阅 [演练：使用 CheckBox 控件更改文档格式](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)。

## <a name="see-also"></a>另请参阅
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [Office UI 自定义](../vsto/office-ui-customization.md)
- [使用扩展对象实现 Word 自动化](../vsto/automating-word-by-using-extended-objects.md)
- [Bookmark 控件](../vsto/bookmark-control.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
