---
title: 演练：使用功能区 XML 创建自定义选项卡
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
ms.openlocfilehash: e05bd9173b83ec3303a058dcf61ea48a7ef7675c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438577"
---
# <a name="walkthrough-create-a-custom-tab-by-using-ribbon-xml"></a>演练：使用功能区 XML 创建自定义选项卡
  本演练演示如何通过创建自定义功能区选项卡**功能区 (XML)** 项。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

 本演练阐释了以下任务：

- 将按钮添加到**外接程序**选项卡。**外接程序**选项卡是功能区 XML 文件中定义的默认选项卡。

- 使用上的按钮实现 Microsoft Office Word 自动化**外接程序**选项卡。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word。

## <a name="create-the-project"></a>创建项目
 第一步是创建 Word VSTO 外接程序项目。 稍后将自定义**外接程序**本文档的选项卡。

### <a name="to-create-a-new-project"></a>创建新项目

1. 创建**Word 外接程序**项目名称**MyRibbonAddIn**。

     有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 此时将打开**ThisAddIn.cs**或**ThisAddIn.vb**代码文件，并添加**MyRibbonAddIn**项目到**解决方案资源管理器**。

## <a name="create-the-vsto-add-ins-tab"></a>创建 VSTO 外接程序选项卡
 若要创建**外接程序**选项卡上，添加**功能区 (XML)** 到你的项目项。 在本演练的稍后部分中，将向此选项卡添加一些按钮。

### <a name="to-create-the-add-ins-tab"></a>若要创建外接程序选项卡

1. 在 **“项目”** 菜单上，单击 **“添加新项”** 。

2. 在中**添加新项**对话框中，选择**功能区 (XML)** 。

3. 将新功能区更名为 **“MyRibbon”** ，然后单击 **“添加”** 。

     **MyRibbon.cs**或**MyRibbon.vb**文件将在设计器中打开。 一个 XML 文件，名为**MyRibbon.xml**也添加到你的项目。

4. 在中**解决方案资源管理器**，右键单击**ThisAddin.cs**或**ThisAddin.vb**，然后单击**查看代码**。

5. 将下面的代码添加到 **ThisAddin** 类中。 此代码可替代 `CreateRibbonExtensibilityObject` 方法，并将功能区 XML 类返回到 Office 应用程序。

     [!code-csharp[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.cs#1)]
     [!code-vb[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.vb#1)]

6. 在中**解决方案资源管理器**，右键单击**MyRibbonAddIn**项目，然后单击**生成**。 验证此项目是否已生成且未发生错误。

## <a name="add-buttons-to-the-add-ins-tab"></a>将按钮添加到外接程序选项卡
 此 VSTO 外接程序旨在为用户提供一种将样板文本和特定表格添加到活动文档的方法。 若要提供用户界面，将添加到两个按钮**外接程序**通过修改功能区 XML 文件的选项卡。 在本演练的稍后部分中，将定义这些按钮的回叫方法。 有关功能区 XML 文件的详细信息，请参阅[功能区 XML](../vsto/ribbon-xml.md)。

### <a name="to-add-buttons-to-the-add-ins-tab"></a>将按钮添加到外接程序选项卡

1. 在中**解决方案资源管理器**，右键单击**MyRibbon.xml** ，然后单击**打开**。

2. 内容替换为**选项卡**具有下面的 XML 元素。 此 XML 更改到的默认控件组的标签**内容**，并添加两个新按钮的标签**插入文本**并**插入表**。

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

## <a name="automate-the-document-by-using-the-buttons"></a>通过使用的按钮自动化文档
 必须添加`onAction`回叫方法**插入文本**并**插入表**按钮以便在用户单击时执行操作。 有关功能区控件的回叫方法的详细信息，请参阅[功能区 XML](../vsto/ribbon-xml.md)。

### <a name="to-add-callback-methods-for-the-buttons"></a>添加按钮的回叫方法

1. 在中**解决方案资源管理器**，右键单击**MyRibbon.cs**或**MyRibbon.vb**，然后单击**打开**。

2. 将以下代码添加到顶部**MyRibbon.cs**或**MyRibbon.vb**文件。 此代码将为 <xref:Microsoft.Office.Interop.Word> 命名空间创建别名。

     [!code-csharp[Trin_RibbonButtons#1](../vsto/codesnippet/CSharp/Trin_RibbonButtons/MyRibbon.cs#1)]
     [!code-vb[Trin_RibbonButtons#1](../vsto/codesnippet/VisualBasic/Trin_RibbonButtons/MyRibbon.vb#1)]

3. 将以下方法添加到 `MyRibbon` 类。 这是回调方法，以**插入文本**将字符串添加到活动文档的游标的当前位置处的按钮。

     [!code-csharp[Trin_Ribbon_Custom_Tab_XML#2](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.cs#2)]
     [!code-vb[Trin_Ribbon_Custom_Tab_XML#2](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.vb#2)]

4. 将以下方法添加到 `MyRibbon` 类。 这是回调方法，以**插入表**将表添加到活动文档中光标的当前位置的按钮。

     [!code-csharp[Trin_Ribbon_Custom_Tab_XML#3](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.cs#3)]
     [!code-vb[Trin_Ribbon_Custom_Tab_XML#3](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.vb#3)]

## <a name="testing-the-vsto-add-in"></a>测试 VSTO 外接程序
 当你运行该项目，将打开 Word 和名为选项卡**外接程序**显示在功能区。 单击**插入文本**并**插入表**上的按钮**外接程序**选项卡以测试代码。

### <a name="to-test-your-vsto-add-in"></a>测试 VSTO 外接程序

1. 按**F5**运行你的项目。

2. 确认**外接程序**会显示在功能区上选项卡。

3. 单击 **“外接程序”** 选项卡。

4. 确认**内容**组是功能区上可见。

5. 单击**插入文本**按钮**内容**组。

     在光标当前位置向文档添加一个字符串。

6. 单击**插入表**按钮**内容**组。

     在光标当前位置向文档添加一个表格。

## <a name="next-steps"></a>后续步骤
 可从以下主题了解有关如何自定义 Office 用户界面的更多信息：

- 自定义功能区的其他 Office 应用程序。 有关支持自定义功能区的应用程序的详细信息，请参阅[功能区概述](../vsto/ribbon-overview.md)。

- 使用功能区设计器自定义 Office 应用程序的功能区。 有关详细信息，请参阅 [Ribbon Designer](../vsto/ribbon-designer.md)。

- 创建自定义操作窗格。 有关详细信息，请参阅[操作窗格概述](../vsto/actions-pane-overview.md)。

- 使用 Outlook 窗体区域自定义 Microsoft Office Outlook 的 UI。 有关详细信息，请参见[演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)。

## <a name="see-also"></a>请参阅
- [功能区概述](../vsto/ribbon-overview.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
