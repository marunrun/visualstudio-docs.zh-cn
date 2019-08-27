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
ms.openlocfilehash: 61c81cef552c18eab5aa737b3460d539abfbdcfc
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63447007"
---
# <a name="ribbon-designer"></a>功能区设计器
  功能区设计器是一个可视化设计画布。 使用功能区设计器将自定义选项卡、 组和控件添加到 Microsoft Office 应用程序的功能区。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

 若要打开功能区设计器，添加**功能区 （可视化设计器）** 到你的项目项。 然后可以执行以下任务使用的设计工具：

- [设计功能区布局](#DesigningRibbonLayout)

- [处理事件并设置控件属性](#HandleEventsSetProperties)

- [将控件添加到 Backstage 视图](#CustomizingMicrosoftOfficeButton)

> [!NOTE]
> 将使用功能区设计器无法完成某些任务。 有关这些任务以及如何实现的详细信息，请参阅[功能区概述](../vsto/ribbon-overview.md)。

 ![视频链接](../vsto/media/playvideo.gif "链接至视频")相关的视频演示，请参阅[如何实现：使用功能区设计器自定义 Outlook 功能区中？](http://go.microsoft.com/fwlink/?LinkID=130312).

## <a name="add-a-ribbon-visual-designer-item-to-a-project"></a>向项目添加功能区 （可视化设计器） 项
 若要使用功能区设计器，添加一个新**功能区 （可视化设计器）** 到你的项目项。 有关详细信息，请参阅[如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)。

 添加一个新**功能区 （可视化设计器）** 项，Visual Studio 会自动添加以下文件到你的项目：

- 功能区代码文件。 此文件的名称为指定的名称**功能区 （可视化设计器）** 中的项**添加新项**对话框。 添加代码以处理对此文件的功能区事件。

- 功能区设计器代码文件。 此文件包含功能区设计器生成的代码，不应直接编辑。

- 资源文件。 此文件包含功能区上的每个控件的属性值。

  如果已有**功能区 （可视化设计器）** 项从另一个项目，您可以重复使用它在当前项目中使用**添加现有项**对话框。

## <a name="DesigningRibbonLayout"></a> 设计功能区
 有三种方法打开功能区设计器：

- 在中**解决方案资源管理器**，双击功能区代码文件。

- 在中**解决方案资源管理器**，右键单击功能区代码文件，并单击**视图设计器**。

- 在中**解决方案资源管理器**，选择功能区代码文件，并单击**设计器**上**视图**菜单。

  功能区设计器包含一个默认选项卡和组。 可以从功能区设计器中删除默认选项卡和组。 若要删除默认组，请右键单击**Group1**，然后单击**删除**。 若要删除默认选项卡，右键单击设计图面的空白区域，然后依次**删除功能区选项卡**。

  此外可以将自定义选项卡、 组和控件添加到功能区设计器。 您可以发现这些控件中的**工具箱**，在**Office 功能区控件**组。 有三种方法来添加控件从**Office 功能区控件**组到功能区设计器：

- 在功能区设计器上将控件拖动到相应的区域中。

- 单击一个控件，然后单击功能区设计器中的相应区域。

- 在设计器中，选择一个合适区域，然后双击中的控件**工具箱**。

### <a name="ribbon-design-workflow"></a>功能区设计工作流
 请按照下列基本步骤来设计功能区布局：

1. [将自定义选项卡添加到功能区](#AddTabToRibbon)。

2. [将组添加到选项卡](#AddGroupsToTab)。

3. [将控件添加到组](#AddControlsToGroups)。

   控件仅可以删除组;不能将控件拖到选项卡直接或功能区。 可以仅在选项卡; 上删除组不能将组拖动到功能区直接。

   通过将其拖动到正确位置来排列控件。 可以通过设置控件的属性**属性**窗口。

   您不能将控件从一个选项卡到另一个功能区上。 如果你想要将控件移动到另一个选项卡，则必须使用**剪切**命令移除该控件从一个选项卡，然后再将粘贴另一个选项卡上的控件。如果执行剪切的控件，并将其粘贴，事件处理程序将停止工作。 你可以重新连接中的事件处理程序**属性**窗口。 有关详细信息，请参阅[属性窗口](../ide/reference/properties-window.md)。

### <a name="AddTabToRibbon"></a> 向功能区添加自定义选项卡
 有三种方法可以向功能区添加自定义选项卡：

- 添加从选项卡**工具箱**。

- 右键单击功能区设计器中，然后依次**添加功能区选项卡**。

- 打开**Tab 集合编辑器**，然后单击**添加**。

   若要打开**Tab 集合编辑器**，在**属性**窗口中，选择**选项卡**属性，然后单击省略号按钮![ASP.NET 移动设计器的椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器椭圆")。

  添加选项卡后，可以添加组以包含控件。

#### <a name="remove-custom-tabs-from-the-ribbon"></a>从功能区中删除自定义选项卡
 有三种方法可以从功能区中删除自定义选项卡：

- 右键单击设计器中，然后依次**删除功能区选项卡**。

- 在中**命令**窗格**属性**窗口中，单击**删除功能区选项卡**。

- 打开**Tab 集合编辑器**，选择选项卡，然后单击**删除**。

#### <a name="change-the-position-of-a-tab-on-the-ribbon"></a>更改功能区上选项卡的位置
 可以更改功能区上的自定义选项卡的顺序。 此外可以将自定义选项卡放置之前或之后在功能区上的内置选项卡。 有关详细信息，请参阅[如何：更改功能区上选项卡的位置](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)。

#### <a name="customize-built-in-tabs-on-the-ribbon"></a>自定义功能区上的内置选项卡
 内置选项卡是已在 Microsoft Office 应用程序的功能区选项卡。 例如，**数据**选项卡是在 Excel 中的内置选项卡。

 可以将组和控件添加到内置选项卡。默认情况下，自定义组显示为内置选项卡上的最后一个组但您可以将其移动任何内置组之前或之后的选项卡上。

 无法移除内置组。

 有关如何自定义内置选项卡的详细信息，请参阅[如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)。

### <a name="AddGroupsToTab"></a> 将组添加到选项卡
 组按照逻辑组织功能区上的控件。 将组添加到选项卡。 将所有其他控件添加到组。

### <a name="AddControlsToGroups"></a> 将控件添加到组
 将一个或多个控件添加到组。 下表描述了每个控件。

|控件|描述|
|-------------|-----------------|
|**Box**|容器组中的控件进行组织。 可以将任何控件添加到除分隔符、 组或选项卡上的框。一个框，可以水平或垂直。|
|**Button**|一个启动操作的按钮。 可以将按钮添加到组、 按钮组、 下拉列表、 库、 菜单或拆分按钮。|
|**ButtonGroup**|包含一个或多个按钮、 切换按钮、 菜单、 拆分按钮和库的组。 可以将按钮组添加到组或菜单。|
|**CheckBox**|一个框，选中或清除要打开或关闭一个选项。|
|**组合框**|一个具有附加列表框的编辑框。 用户可以键入或者选择其选项。 该框显示当前所选内容。 使用<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.Items%2A>属性来添加和删除在运行时的项之前或之后在功能区加载到 Office 应用程序。|
|**DropDown**|用户可以选择的项的列表。 用户不能在下拉列表中键入新项。<br /><br /> 使用<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.Items%2A>属性将项添加到列表。 可以添加和删除项目在运行时。<br /><br /> 使用<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.Buttons%2A>属性来将按钮添加到列表。 但是，不能添加，并在运行时在功能区加载到 Office 应用程序之后删除按钮。|
|**EditBox**|一个框，用户可以在其中键入文本。|
|**Gallery**|一个菜单，提供的数组或网格的用户可以从中选择的可视化选项。 您可以控制菜单中的选项的布局。 使用<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ColumnCount%2A>和<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.RowCount%2A>属性以指定的行和列将显示的项目数和库的按钮。|
|**标签**|可用于标识功能区上的控件的文本。|
|**菜单**|下拉列表可以包含任何以下控件：<br /><br /> -按钮<br />-复选框<br />库<br />-菜单<br />拆分按钮<br />-切换按钮<br />-   Separator<br /><br /> 若要将控件添加到功能区设计器中的菜单中，单击菜单来公开菜单设计图面中的向下箭头。 然后，可以将功能区控件从**工具箱**拖至菜单。 若要排列控件，请将它们拖动至所需位置。<br /><br /> 若要将控件添加到<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>功能区加载到 Office 应用程序后，必须设置<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.Dynamic%2A>属性设置为**true**功能区加载之前。 有关如何执行此操作的信息，请参阅[功能区对象模型概述](../vsto/ribbon-object-model-overview.md)。|
|**分隔符**|用于分隔列表中的项细条形图。 添加到组时，该线条是垂直的。 添加到菜单时，该线条是水平。|
|**SplitButton**|一个具有附加菜单按钮。 拆分按钮可以包含任何以下控件：<br /><br /> -按钮<br />-复选框<br />库<br />-菜单<br />拆分按钮<br />-切换按钮<br />-   Separator<br /><br /> 菜单上，与拆分按钮有其自己的设计图面。 但是，与不同的菜单中，你只能在功能区加载到 Office 应用程序之前更新拆分按钮中的项。 有关如何更新拆分按钮中的项的信息，请参阅[功能区对象模型概述](../vsto/ribbon-object-model-overview.md)。|
|**ToggleButton**|将出现一个按钮按下或未按下状态。|

## <a name="HandleEventsSetProperties"></a> 处理事件和设置属性
 功能区设计器，可使用在设计时设置控件属性**属性**窗口。 此外，在功能区公开可用于获取和设置在运行时的功能区控件的属性的强类型化的对象模型。

 你可以双击要打开该控件的默认事件的事件处理程序的设计器上的任何控件。 可以使用创建的所有其他控件事件的事件处理程序**属性**窗口。

 功能区事件和属性中的位置<xref:Microsoft.Office.Tools.Ribbon>命名空间。 **功能区 （可视化设计器）** 项会自动在项目中添加对此程序集的引用，并插入适当**使用**或**导入**顶部的语句功能区代码文件。

 有关处理功能区事件和在运行时设置功能区控件的属性的信息，请参阅[功能区对象模型概述](../vsto/ribbon-object-model-overview.md)。

## <a name="CustomizingMicrosoftOfficeButton"></a> 自定义 Backstage 视图
 可以使用功能区设计器将控件添加到单击时打开的菜单**文件**选项卡。此菜单称为 Backstage 视图。

 使用功能区设计器，无法在内置控件前后放置控件。 内置控件是已出现在 Backstage 视图中的控件。 如果你想要在内置控件前后放置控件，必须使用功能区 XML。 有关详细信息**功能区 (XML)**，请参阅[功能区 XML](../vsto/ribbon-xml.md)。 有关自定义 Backstage 视图的详细信息，请参阅[开发人员的 Office 2010 Backstage 视图简介](http://go.microsoft.com/fwlink/?LinkId=182189)并[自定义开发人员的 Office 2010 Backstage 视图](http://go.microsoft.com/fwlink/?LinkId=182188)。

 [!INCLUDE[appliesto_ribbon_2010](../vsto/includes/appliesto-ribbon-2010-md.md)]

 有关如何将控件添加到 Backstage 视图的信息，请参阅[如何：将控件添加到 Backstage 视图](../vsto/how-to-add-controls-to-the-backstage-view.md)。

## <a name="Accessibility"></a> 功能区设计器中的辅助功能
 可以使用键盘快捷键在功能区设计器中移动控件。 某些键盘快捷键适用于所有控件，而某些仅适用于具有菜单的控件。

 适用于所有控件的键盘快捷键表所示。

|操作|键盘快捷键|
|------------|-----------------------|
|在列表中移动之前的上一个控件的控件。|**Ctrl**+**Up**<br /><br /> **Ctrl**+**Left**|
|将一个控件移动后在列表中的下一个控件。|**Ctrl**+**Down**<br /><br /> **Ctrl**+**Right**|
|所选内容从一个控件移动到另一个相同的组中。 对于下拉面板中，移动父控件与下拉面板中的控件之间。|**最多**<br /><br /> **向下**|
|向前循环访问所有控件。|Tab|
|所有控件向后循环访问。|**Shift**+**Tab**|
|删除选定的控件或一组控件。|**删除**|
|复制选定的控件。|Ctrl+C|
|剪切选定的控件。|Ctrl+X|
|粘贴剪贴板中的控件。|Ctrl+V|
|选择**工具箱**。|**Ctrl**+**Alt**+**X**|
|选择父组件。|**Esc**|

 仅适用于 Microsoft Office 菜单的键盘快捷键<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>，和<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>下表中所示。

|操作|键盘快捷键|
|------------|-----------------------|
|如果下拉面板已打开并且没有下拉面板上选择一个控件，请选择父控件。|左侧|
|如果下拉面板已打开，并且父控件处于选中状态，则关闭下拉面板。|左侧|
|打开下拉面板。|右侧|
|如果下拉面板已打开，请选择下拉面板上的第一个控件。|右侧|
|关闭下拉面板。|**Esc**|

## <a name="see-also"></a>请参阅

- [功能区概述](../vsto/ribbon-overview.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [如何：将功能区从功能区设计器导出到功能区 XML](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [在运行时在功能区的访问](../vsto/accessing-the-ribbon-at-run-time.md)
