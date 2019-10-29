---
title: 功能区设计器
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- Designer_Microsoft.VisualStudio.Tools.Office.Ribbon.Design.RibbonDesigner
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, about Ribbon Designer
- controls [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], controls
- customizing the Ribbon, about Ribbon Designer
- Ribbon [Office development in Visual Studio], visual designer
- customizing the Ribbon
- custom Ribbon
- designers [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], customizing
- Ribbon [Office development in Visual Studio], common tasks
- Ribbon Designer [Office development in Visual Studio]
- read-only properties
- Ribbon [Office development in Visual Studio], shortcut keys
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e1c2941b0c088a832540fd3380c993fe2c380b44
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985626"
---
# <a name="ribbon-designer"></a>功能区设计器
  功能区设计器是一个可视化设计画布。 使用功能区设计器将自定义选项卡、组和控件添加到 Microsoft Office 应用程序的功能区。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

 若要打开功能区设计器，请将 "**功能区（可视化设计器）** " 项添加到项目。 然后，您可以对以下任务使用设计工具：

- [设计功能区布局](#DesigningRibbonLayout)

- [处理事件和设置控件属性](#HandleEventsSetProperties)

- [向 Backstage 视图添加控件](#CustomizingMicrosoftOfficeButton)

> [!NOTE]
> 某些任务无法通过使用功能区设计器完成。 有关这些任务以及如何完成这些任务的详细信息，请参阅[功能区概述](../vsto/ribbon-overview.md)。

## <a name="add-a-ribbon-visual-designer-item-to-a-project"></a>将 "功能区（可视化设计器）" 项添加到项目
 若要使用功能区设计器，请将新的 "**功能区（可视化设计器）** " 项添加到项目。 有关详细信息，请参阅[如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)。

 添加新的 "**功能区（可视化设计器）** " 项时，Visual Studio 会自动将以下文件添加到项目中：

- 功能区代码文件。 此文件具有你在 "**添加新项**" 对话框中为 "**功能区（可视化设计器）** " 项指定的名称。 将用于处理功能区事件的代码添加到此文件。

- 功能区设计器代码文件。 此文件包含由功能区设计器生成的代码，不应直接编辑。

- 资源文件。 此文件包含功能区上每个控件的属性值。

  如果已经有一个来自其他项目的 "**功能区（可视化设计器）** " 项，则可以使用 "**添加现有项**" 对话框在当前项目中重复使用它。

## <a name="DesigningRibbonLayout"></a>设计功能区
 可以通过三种方式打开功能区设计器：

- 在**解决方案资源管理器**中，双击功能区代码文件。

- 在**解决方案资源管理器**中，右键单击功能区代码文件，然后单击 "**视图设计器**"。

- 在**解决方案资源管理器**中，选择功能区代码文件，然后在 "**视图**" 菜单上单击 "**设计器**"。

  功能区设计器包含一个默认选项卡和组。 可以从功能区设计器中删除默认选项卡和组。 若要删除默认组，请右键单击 " **Group1**"，然后单击 "**删除**"。 若要删除默认选项卡，请右键单击设计图面的空白区域，然后单击 "**删除功能区选项卡**"。

  你还可以将自定义选项卡、组和控件添加到功能区设计器。 可以在 " **Office 功能区控件**" 组中的 "**工具箱**" 中找到这些控件。 有三种方法可将 " **Office 功能区控件**" 组中的控件添加到功能区设计器：

- 将控件拖动到功能区设计器中的相应区域。

- 单击控件，然后单击功能区设计器中的相应区域。

- 在设计器中选择相应的区域，然后双击**工具箱**中的控件。

### <a name="ribbon-design-workflow"></a>功能区设计工作流
 按照以下基本步骤来设计功能区布局：

1. [向功能区添加自定义选项卡](#AddTabToRibbon)。

2. [将组添加到选项卡](#AddGroupsToTab)。

3. [向组中添加控件](#AddControlsToGroups)。

   只能对组删除控件;不能将控件直接拖到选项卡或功能区。 只能在选项卡上删除组;不能将组直接拖到功能区。

   通过将控件拖动到正确的位置来排列控件。 您可以使用 "**属性**" 窗口设置控件的属性。

   在功能区上，不能将控件从一个选项卡拖动到另一个选项卡。 如果要将控件移动到另一个选项卡，则必须使用 "**剪切**" 命令从一个选项卡中删除该控件，然后将该控件粘贴到另一个选项卡上。如果确实剪切并粘贴控件，事件处理程序将停止工作。 您可以在 "**属性**" 窗口中重新连接事件处理程序。 有关详细信息，请参阅[属性窗口](../ide/reference/properties-window.md)。

### <a name="AddTabToRibbon"></a>向功能区添加自定义选项卡
 向功能区添加自定义选项卡的方法有三种：

- 从**工具箱**添加一个选项卡。

- 右键单击功能区设计器，然后单击 "**添加功能区选项卡**"。

- 打开 " **Tab 集合编辑器**"，然后单击 "**添加**"。

   若要打开 " **Tab 集合编辑器**"，请在 "**属性**" 窗口中选择 "**选项卡**" 属性，然后单击省略号按钮 " ![ASP.NET Mobile 设计器](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")" "椭圆形"。

  添加选项卡后，可以添加组以包含控件。

#### <a name="remove-custom-tabs-from-the-ribbon"></a>从功能区移除自定义选项卡
 有三种方法可从功能区中删除自定义选项卡：

- 右键单击设计器，然后单击 "**删除功能区选项卡**"。

- 在 "**属性**" 窗口的 "**命令**" 窗格中，单击 "**删除功能区选项卡**"。

- 打开 " **Tab 集合编辑器**"，选择选项卡，然后单击 "**删除**"。

#### <a name="change-the-position-of-a-tab-on-the-ribbon"></a>更改功能区上选项卡的位置
 您可以更改功能区上自定义选项卡的顺序。 您还可以将自定义选项卡定位在功能区上的内置选项卡之前或之后。 有关详细信息，请参阅[如何：更改选项卡在功能区上的位置](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)。

#### <a name="customize-built-in-tabs-on-the-ribbon"></a>自定义功能区上的内置选项卡
 内置选项卡是 Microsoft Office 应用程序的功能区上已经存在的选项卡。 例如，"**数据**" 选项卡是 Excel 中的内置选项卡。

 可以将组和控件添加到内置选项卡。默认情况下，自定义组在内置选项卡上显示为最后一个组，但您可以在选项卡上的任何内置组之前或之后移动该选项卡。

 不能删除内置组。

 有关如何自定义内置选项卡的详细信息，请参阅[如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)。

### <a name="AddGroupsToTab"></a>将组添加到选项卡
 组以逻辑方式组织功能区上的控件。 将组添加到选项卡。 将所有其他控件添加到组。

### <a name="AddControlsToGroups"></a>向组中添加控件
 向组中添加一个或多个控件。 下表对每个控件进行了说明。

|控件|描述|
|-------------|-----------------|
|**Box**|用于组织组中的控件的容器。 您可以向框添加除分隔符、组或选项卡之外的任何控件。框可以是水平或垂直。|
|**Button**|用于启动操作的按钮。 您可以将按钮添加到组、按钮组、下拉列表、库、菜单或拆分按钮。|
|**ButtonGroup**|一个组，其中包含一个或多个按钮、切换按钮、菜单、拆分按钮和库。 可以将按钮组添加到组或菜单。|
|**CheckBox**|选中或清除以打开或关闭选项的复选框。|
|**组合框**|已附加列表框的编辑框。 用户可以键入或选择其选择。 该框显示当前选定内容。 使用 <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.Items%2A> 属性可以在功能区加载到 Office 应用程序之前或之后在运行时添加和移除项。|
|**DropDown**|用户可以选择的项的列表。 用户不能在下拉列表中键入新项。<br /><br /> 使用 <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.Items%2A> 属性可向列表中添加项。 您可以在运行时添加和移除项。<br /><br /> 使用 <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.Buttons%2A> 属性可向列表中添加按钮。 但是，在功能区加载到 Office 应用程序中之后，不能在运行时添加和删除按钮。|
|**"编辑框**|一个框，用户可以在其中键入文本。|
|**库**|一个菜单，该菜单显示用户可从中选择的可视化选项的数组或网格。 可以在菜单中控制选择的布局。 使用 "<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ColumnCount%2A>" 和 "<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.RowCount%2A>" 属性来指定将显示库的项和按钮的行数和列数。|
|**标签**|可以用来标识功能区上控件的文本。|
|**菜单**|一个下拉列表，其中可以包含以下任何控件：<br /><br /> -按钮<br />-复选框<br />-库<br />-菜单<br />-拆分按钮<br />-切换按钮<br />-分隔符<br /><br /> 若要将控件添加到功能区设计器中的菜单，请单击菜单中的向下箭头以显示菜单设计图面。 然后，您可以将功能区控件从**工具箱**拖至菜单上。 若要排列控件，请将其拖到所需的位置。<br /><br /> 若要在功能区加载到 Office 应用程序中之后将控件添加到 <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>，则在加载功能区之前必须将 <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.Dynamic%2A> 属性设置为**true** 。 有关如何执行此操作的信息，请参阅[功能区对象模型概述](../vsto/ribbon-object-model-overview.md)。|
|**分隔符**|用于分隔列表中的项的窄条。 添加到组时，条形是垂直的。 添加到菜单时，条形是水平的。|
|**SplitButton**|附加了菜单的按钮。 拆分按钮可以包含以下任何控件：<br /><br /> -按钮<br />-复选框<br />-库<br />-菜单<br />-拆分按钮<br />-切换按钮<br />-分隔符<br /><br /> 与菜单类似，"拆分" 按钮具有其自己的设计图面。 但是，与菜单不同，在功能区加载到 Office 应用程序中之前，只能更新拆分按钮中的项。 有关如何更新拆分按钮中的项的信息，请参阅[功能区对象模型概述](../vsto/ribbon-object-model-overview.md)。|
|**按钮**|显示为按下或未按下的按钮。|

## <a name="HandleEventsSetProperties"></a>处理事件和设置属性
 功能区设计器使您能够通过使用 "**属性**" 窗口在设计时设置控件属性。 此外，功能区公开了一个强类型对象模型，可用于在运行时获取和设置功能区控件的属性。

 您可以双击设计器上的任何控件，打开控件的默认事件的事件处理程序。 您可以使用 "**属性**" 窗口为所有其他控件事件创建事件处理程序。

 功能区事件和属性位于 <xref:Microsoft.Office.Tools.Ribbon> 命名空间中。 "**功能区（可视化设计器）** " 项会自动在项目中添加对此程序集的引用，并在功能区代码文件的顶部插入适当的**using**或**Imports**语句。

 有关处理功能区事件和在运行时设置功能区控件的属性的信息，请参阅[功能区对象模型概述](../vsto/ribbon-object-model-overview.md)。

## <a name="CustomizingMicrosoftOfficeButton"></a>自定义 Backstage 视图
 您可以使用功能区设计器将控件添加到单击 "**文件**" 选项卡时打开的菜单。此菜单称为 Backstage 视图。

 不能使用功能区设计器在内置控件之前或之后放置控件。 内置控件是已在 Backstage 视图中显示的控件。 如果要将控件放置在内置控件之前或之后，必须使用功能区 XML。 有关**功能区（xml）** 的详细信息，请参阅[功能区 XML](../vsto/ribbon-xml.md)。 有关自定义 Backstage 视图的详细信息，请参阅面向[开发人员的 office 2010 backstage 视图的简介](/previous-versions/office/developer/office-2010/ee691833(v=office.14))和[为开发人员自定义 office 2010 backstage 视图](/previous-versions/office/developer/office-2010/ee815851(v=office.14))。

 [!INCLUDE[appliesto_ribbon_2010](../vsto/includes/appliesto-ribbon-2010-md.md)]

 有关如何向 Backstage 视图添加控件的信息，请参阅[如何：向 backstage 视图添加控件](../vsto/how-to-add-controls-to-the-backstage-view.md)。

## <a name="Accessibility"></a>功能区设计器中的辅助功能
 您可以使用键盘快捷方式在功能区设计器中移动控件。 某些键盘快捷方式适用于所有控件，有些快捷方式仅适用于具有菜单的控件。

 下表显示了适用于所有控件的键盘快捷方式。

|操作|键盘快捷方式|
|------------|-----------------------|
|将控件移动到列表中上一个控件之前。|**Ctrl** **向上**+<br /><br /> **Ctrl**+**向左**|
|将控件移动到列表中的下一个控件之后。|**Ctrl**+**向下**<br /><br /> **Ctrl**+**向右**|
|将所选内容从一个控件移到同一个组中的另一个控件。 对于下拉面板，请在父控件和下拉面板中的控件之间移动。|**Up**<br /><br /> **分解**|
|向前循环访问所有控件。|Tab|
|循环访问所有控件。|**Shift**+**Tab**|
|删除所选的一个或一组控件。|**删除**|
|复制选定的控件。|Ctrl+C|
|剪切选定的控件。|Ctrl+X|
|从剪贴板粘贴控件。|Ctrl+V|
|选择 "**工具箱**"。|**Ctrl**+**Alt**+**X**|
|选择父组件。|Esc|

 下表显示了仅适用于 Microsoft Office 菜单、<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>和 <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton> 的键盘快捷方式。

|操作|键盘快捷方式|
|------------|-----------------------|
|如果下拉面板已打开，并且在下拉面板上选择了控件，则选择父控件。|左侧|
|如果下拉面板处于打开状态并且选中了父控件，则关闭下拉面板。|左侧|
|打开下拉面板。|右侧|
|如果下拉面板已打开，请选择下拉面板上的第一个控件。|右侧|
|关闭下拉面板。|Esc|

## <a name="see-also"></a>请参阅

- [功能区概述](../vsto/ribbon-overview.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [如何：将功能区从功能区设计器导出到功能区 XML](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [在运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)
