---
title: 在运行时在 VSTO 外接程序项目中向工作表添加控件
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], adding controls
- controls [Office development in Visual Studio], adding to worksheets at run time
- application-level add-ins [Office development in Visual Studio], adding controls
- worksheets, adding controls at run time
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5bf2610ca1f3f3767082bf50953f821d37d1af2a
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71253898"
---
# <a name="walkthrough-add-controls-to-a-worksheet-at-run-time-in-vsto-add-in-project"></a>演练：在运行时在 VSTO 外接程序项目中向工作表添加控件
  可通过使用 Excel VSTO 外接程序向任何打开的工作表添加控件。 本演练演示如何利用功能区使用户能够向工作表添加 <xref:Microsoft.Office.Tools.Excel.Controls.Button>、<xref:Microsoft.Office.Tools.Excel.NamedRange> 和 <xref:Microsoft.Office.Tools.Excel.ListObject>。 有关信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

 **适用于:** 本主题中的信息适用于 Excel 的 VSTO 外接程序项目。 有关详细信息，请参阅 [Features Available by Office Application and Project Type](../vsto/features-available-by-office-application-and-project-type.md)。

 本演练阐释了以下任务：

- 提供用于将控件添加到工作表的用户界面 (UI)。

- 将控件添加到工作表。

- 从工作表中移除控件。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Excel

## <a name="create-a-new-excel-vsto-add-in-project"></a>创建新的 Excel VSTO 外接程序项目
 首先创建 Excel VSTO 外接程序项目。

### <a name="to-create-a-new-excel-vsto-add-in-project"></a>若要新建 Excel VSTO 外接程序项目

1. 在[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中，创建一个名为**ExcelDynamicControls**的 Excel VSTO 外接程序项目。 有关详细信息，请参阅[如何：在 Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)中创建 Office 项目。

2. 添加对 "" 的**引用，然后**添加对 "" 的引用。 在本演练稍后内容中，需要此引用以编程方式将 Windows 窗体控件添加到工作表。

## <a name="provide-a-ui-to-add-controls-to-a-worksheet"></a>提供向工作表添加控件的 UI
 添加自定义选项卡到 Excel 功能区。 用户可以选中选项卡上的复选框，以向工作表添加控件。

#### <a name="to-provide-a-ui-to-add-controls-to-a-worksheet"></a>若要提供用于将控件添加到工作表的 UI

1. 在 **“项目”** 菜单上，单击 **“添加新项”** 。

2. 在 "**添加新项**" 对话框中，选择 "**功能区（可视化设计器）** "，然后单击 "**添加**"。

     在功能区设计器中打开名为**Ribbon1.cs**或**ribbon1.mfcribbon-ms**的文件，并显示默认选项卡和组。

3. 从 "**工具箱**" 的 " **Office 功能区控件**" 选项卡中，将 "CheckBox" 控件拖到 " **group1**"。

4. 单击 **CheckBox1** 以将其选中。

5. 在 **“属性”** 窗口中，更改下列属性。

    |Property|值|
    |--------------|-----------|
    |**Name**|**Button**|
    |**标签**|**Button**|

6. 将第二个复选框添加到 **group1**，然后更改下列属性。

    |Property|值|
    |--------------|-----------|
    |**Name**|**NamedRange**|
    |**标签**|**NamedRange**|

7. 将第三个复选框添加到**group1**，然后更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**Name**|**ListObject**|
    |**标签**|**ListObject**|

## <a name="add-controls-to-the-worksheet"></a>向工作表添加控件
 托管的控件只能添加到主机项，充当容器。 因为 VSTO 外接程序项目使用任何打开的工作簿，所以 VSTO 外接程序会将工作表转换为主机项，或获取现有的主机项，然后才添加控件。 将代码添加到每个控件的单击事件处理程序中以生成基于打开的工作表的 <xref:Microsoft.Office.Tools.Excel.Worksheet> 主机项。 然后，在工作表当前所选内容中添加 <xref:Microsoft.Office.Tools.Excel.Controls.Button>、<xref:Microsoft.Office.Tools.Excel.NamedRange> 和 <xref:Microsoft.Office.Tools.Excel.ListObject>。

### <a name="to-add-controls-to-a-worksheet"></a>若要向工作表添加控件

1. 在功能区设计器中，双击 "**按钮**"。

     "**按钮**" 复选框的事件处理程序将在代码编辑器中打开。<xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click>

2. 将 `Button_Click` 事件处理程序替换为以下代码。

     此代码使用 `GetVstoObject` 方法获取表示工作薄中第一个工作表的主机项，然后将 <xref:Microsoft.Office.Tools.Excel.Controls.Button> 控件添加到当前选定的单元格。

     [!code-csharp[Trin_Excel_Dynamic_Controls#2](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs#2)]
     [!code-vb[Trin_Excel_Dynamic_Controls#2](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb#2)]

3. 在**解决方案资源管理器**中，选择 " *Ribbon1.cs* " 或 " *ribbon1.mfcribbon-ms*"。

4. 在 "**视图**" 菜单上，单击 "**设计器**"。

5. 在功能区设计器中，双击 " **NamedRange**"。

6. 将 `NamedRange_Click` 事件处理程序替换为以下代码。

     此代码使用 `GetVstoObject` 方法获取表示工作簿中第一个工作表的主机项，然后为当前选定的单元格定义 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件。

     [!code-csharp[Trin_Excel_Dynamic_Controls#3](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs#3)]
     [!code-vb[Trin_Excel_Dynamic_Controls#3](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb#3)]

7. 在功能区设计器中，双击 " **ListObject**"。

8. 将 `ListObject_Click` 事件处理程序替换为以下代码。

     此代码使用 `GetVstoObject` 方法获取表示工作薄中第一个工作表的主机项，然后为当前选定的单元格定义 <xref:Microsoft.Office.Tools.Excel.ListObject>。

     [!code-csharp[Trin_Excel_Dynamic_Controls#4](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs#4)]
     [!code-vb[Trin_Excel_Dynamic_Controls#4](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb#4)]

9. 将下面的语句添加到功能区代码文件的顶部。

     [!code-csharp[Trin_Excel_Dynamic_Controls#1](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs#1)]
     [!code-vb[Trin_Excel_Dynamic_Controls#1](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb#1)]

## <a name="remove-controls-from-the-worksheet"></a>从工作表中移除控件
 保存并关闭工作表时，不会保留控件。 保存工作表之前应以编程方式移除所有生成的 Windows 窗体控件，否则再次打开工作薄时，将仅出现控件的边框。 将代码添加到用于从生成的主机项的控件集合中移除 Windows 窗体控件的 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> 事件中。 有关详细信息，请参阅[在 Office 文档中保存动态控件](../vsto/persisting-dynamic-controls-in-office-documents.md)。

### <a name="to-remove-controls-from-the-worksheet"></a>若要从工作表中移除控件

1. 在**解决方案资源管理器**中，选择 " *ThisAddIn.cs* " 或 " *ThisAddIn*"。

2. 在 "**视图**" 菜单上，单击 "**代码**"。

3. 将以下方法添加到 `ThisAddIn` 类。 此代码会获取工作簿中的第一个工作表，然后使用 `HasVstoObject` 方法检查该工作表是否含有生成的工作表项目。 如果生成的工作表对象中含有控件，则该代码会获取工作表项目并循环访问控件集合，从而移除控件。

     [!code-csharp[Trin_Excel_Dynamic_Controls#6](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#6)]
     [!code-vb[Trin_Excel_Dynamic_Controls#6](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb#6)]

4. 在 C# 中，必须为 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> 事件创建一个事件处理程序。 你可以将此代码放置在 `ThisAddIn_Startup` 方法中。 有关创建事件处理程序的详细信息， [请参阅如何：在 Office 项目](../vsto/how-to-create-event-handlers-in-office-projects.md)中创建事件处理程序。 将 `ThisAddIn_Startup` 方法替换为以下代码。

     [!code-csharp[Trin_Excel_Dynamic_Controls#5](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#5)]

## <a name="test-the-solution"></a>测试解决方案
 通过从功能区上的自定义选项卡中选择控件，将控件添加到工作表。 保存该工作表时，这些控件也随之移除。

### <a name="to-test-the-solution"></a>若要测试解决方案。

1. 按**F5**运行项目。

2. 在 Sheet1 中选择任意单元格。

3. 单击 **“外接程序”** 选项卡。

4. 在 " **group1** " 组中，单击 "**按钮**"。

     选定的单元格中会出现一个按钮。

5. 在 Sheet1 中选择不同的单元格。

6. 在 " **group1** " 组中，单击 " **NamedRange**"。

     则会为选定的单元格定义命名范围。

7. 在 Sheet1 中选择一系列单元格。

8. 在 " **group1** " 组中，单击 " **ListObject**"。

     则会为选定的单元格添加列表对象。

9. 保存该工作表。

     添加到 Sheet1 的控件将不再出现。

## <a name="next-steps"></a>后续步骤
 你可以从此主题中了解关于 Excel VSTO 外接程序项目中控件的详细信息：

- 若要了解如何将控件保存到工作表中，请参阅[Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)中的 Excel VSTO 外接程序动态控件示例。

## <a name="see-also"></a>请参阅
- [Excel 解决方案](../vsto/excel-solutions.md)
- [Office 文档上的 Windows 窗体控件概述](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [ListObject 控件](../vsto/listobject-control.md)
