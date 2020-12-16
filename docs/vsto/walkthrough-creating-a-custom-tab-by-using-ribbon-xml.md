---
title: 演练：使用功能区 XML 创建自定义选项卡
description: 了解如何将按钮添加到 Add-Ins 选项卡，以及如何使用功能区 (XML) 自动完成 Microsoft Word。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], tabs
- customizing the Ribbon, tabscustom Ribbon, tabs
- Ribbon [Office development in Visual Studio], XML
- XML [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], customizing
- Custom tab [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e81d20dc179df76b759223c1460ca13bfceb5706
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97524875"
---
# <a name="walkthrough-create-a-custom-tab-by-using-ribbon-xml"></a>演练：使用功能区 XML 创建自定义选项卡
  本演练演示如何使用 **功能区 (XML)** 项创建自定义功能区选项卡。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

 本演练演示以下任务：

- 将按钮添加到 " **外接程序** " 选项卡。" **外接程序** " 选项卡是功能区 XML 文件中定义的默认选项卡。

- 使用 " **外接程序** " 选项卡上的按钮自动 Microsoft Office 单词。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word。

## <a name="create-the-project"></a>创建项目
 第一步是创建 Word VSTO 外接程序项目。 稍后将自定义此文档的 " **外接程序** " 选项卡。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 创建名为 **MyRibbonAddIn** 的 **Word 外接程序** 项目。

     有关详细信息，请参阅 [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 打开 **ThisAddIn.cs** 或 **ThisAddIn** 代码文件，并将 **MyRibbonAddIn** 项目添加到 **解决方案资源管理器**。

## <a name="create-the-vsto-add-ins-tab"></a>创建 VSTO 外接程序选项卡
 若要创建 " **外接程序** " 选项卡，请在项目中添加一个 **(XML) 项的功能区** 。 在本演练的稍后部分中，将向此选项卡添加一些按钮。

### <a name="to-create-the-add-ins-tab"></a>创建 "外接程序" 选项卡

1. 在 **“项目”** 菜单上，单击 **“添加新项”**。

2. 在 " **添加新项** " 对话框中，选择 " **功能区 (XML)**。

3. 将新功能区更名为 **“MyRibbon”**，然后单击 **“添加”**。

     **MyRibbon.cs** 或 **myribbon.vb** 文件将在设计器中打开。 名为 **MyRibbon.xml** 的 XML 文件也会添加到你的项目中。

4. 在 **解决方案资源管理器** 中，右键单击 " **ThisAddin.cs** " 或 " **ThisAddin**"，然后单击 " **查看代码**"。

5. 将下面的代码添加到 **ThisAddin** 类中。 此代码可替代 `CreateRibbonExtensibilityObject` 方法，并将功能区 XML 类返回到 Office 应用程序。

     [!code-csharp[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.cs#1)]
     [!code-vb[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.vb#1)]

6. 在 **解决方案资源管理器** 中，右键单击 **MyRibbonAddIn** 项目，然后单击 " **生成**"。 验证此项目是否已生成且未发生错误。

## <a name="add-buttons-to-the-add-ins-tab"></a>将按钮添加到 "外接程序" 选项卡
 此 VSTO 外接程序旨在为用户提供一种将样板文本和特定表格添加到活动文档的方法。 若要提供用户界面，请通过修改功能区 XML 文件将两个按钮添加到 " **外接程序** " 选项卡。 在本演练的稍后部分中，将定义这些按钮的回叫方法。 有关功能区 XML 文件的详细信息，请参阅 [功能区 xml](../vsto/ribbon-xml.md)。

### <a name="to-add-buttons-to-the-add-ins-tab"></a>将按钮添加到 "外接程序" 选项卡

1. 在 **解决方案资源管理器** 中，右键单击 **MyRibbon.xml** ，然后单击 " **打开**"。

2. 将 **选项卡** 元素的内容替换为以下 XML。 此 XML 将默认控件组的标签更改为 " **内容**"，并添加两个带有 "标签" " **插入文本** " 和 " **插入表格**" 的新按钮。

    ```xml
    <tab idMso="TabAddIns">
        <group id="ContentGroup" label="Content">
            <button id="textButton" label="Insert Text"
                 screentip="Text" onAction="OnTextButton"
                 supertip="Inserts text at the cursor location."/>
            <button id="tableButton" label="Insert Table"
                 screentip="Table" onAction="OnTableButton"
                 supertip="Inserts a table at the cursor location."/>
        </group>
    </tab>
    ```

## <a name="automate-the-document-by-using-the-buttons"></a>使用按钮自动执行文档
 您必须 `onAction` 为 " **插入文本** " 和 " **插入表格** " 按钮添加回调方法，以便在用户单击时执行操作。 有关功能区控件的回叫方法的详细信息，请参阅 [功能区 XML](../vsto/ribbon-xml.md)。

### <a name="to-add-callback-methods-for-the-buttons"></a>添加按钮的回叫方法

1. 在 **解决方案资源管理器** 中，右键单击 **MyRibbon.cs** 或 **Myribbon.vb**，然后单击 " **打开**"。

2. 将以下代码添加到 **MyRibbon.cs** 或 **myribbon.vb** 文件的顶部。 此代码将为 <xref:Microsoft.Office.Interop.Word> 命名空间创建别名。

     [!code-csharp[Trin_RibbonButtons#1](../vsto/codesnippet/CSharp/Trin_RibbonButtons/MyRibbon.cs#1)]
     [!code-vb[Trin_RibbonButtons#1](../vsto/codesnippet/VisualBasic/Trin_RibbonButtons/MyRibbon.vb#1)]

3. 将以下方法添加到 `MyRibbon` 类。 这是 " **插入文本** " 按钮的回调方法，用于在光标当前位置向活动文档添加字符串。

     [!code-csharp[Trin_Ribbon_Custom_Tab_XML#2](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.cs#2)]
     [!code-vb[Trin_Ribbon_Custom_Tab_XML#2](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.vb#2)]

4. 将以下方法添加到 `MyRibbon` 类。 这是 " **插入表格** " 按钮的回叫方法，用于在光标当前位置向活动文档添加表。

     [!code-csharp[Trin_Ribbon_Custom_Tab_XML#3](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.cs#3)]
     [!code-vb[Trin_Ribbon_Custom_Tab_XML#3](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.vb#3)]

## <a name="testing-the-vsto-add-in"></a>测试 VSTO 外接程序
 运行该项目时，Word 将打开，并在功能区上显示名为 " **外接程序** " 的选项卡。 单击 "**外接程序**" 选项卡上的 "**插入文本**" 和 "**插入表格**" 按钮以测试代码。

### <a name="to-test-your-vsto-add-in"></a>测试 VSTO 外接程序

1. 按 **F5** 运行项目。

2. 确认 " **外接程序** " 选项卡在功能区上可见。

3. 单击 **“外接程序”** 选项卡。

4. 确认 " **内容** " 组在功能区上可见。

5. 单击 **内容** 组中的 "**插入文本**" 按钮。

     在光标当前位置向文档添加一个字符串。

6. 单击 **内容** 组中的 "**插入表格**" 按钮。

     在光标当前位置向文档添加一个表格。

## <a name="next-steps"></a>后续步骤
 可从以下主题了解有关如何自定义 Office 用户界面的更多信息：

- 自定义不同 Office 应用程序的功能区。 有关支持自定义功能区的应用程序的详细信息，请参阅 [功能区概述](../vsto/ribbon-overview.md)。

- 使用功能区设计器自定义 Office 应用程序的功能区。 有关详细信息，请参阅 [Ribbon Designer](../vsto/ribbon-designer.md)。

- 创建自定义操作窗格。 有关详细信息，请参阅 [操作窗格概述](../vsto/actions-pane-overview.md)。

- 使用 Outlook 窗体区域自定义 Microsoft Office Outlook 的 UI。 有关详细信息，请参阅 [演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)。

## <a name="see-also"></a>另请参阅
- [功能区概述](../vsto/ribbon-overview.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
