---
title: 功能区对象模型概述
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], object model
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6ca22704345fefb4944bda7dd9f71942fe8dfb50
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71256017"
---
# <a name="ribbon-object-model-overview"></a>功能区对象模型概述
  [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]公开了一个强类型对象模型，可用于在运行时获取和设置功能区控件的属性。 例如，可以动态填充菜单控件，或显示和隐藏控件根据上下文。 你还可以将选项卡、组和控件添加到功能区，但在 Office 应用程序加载功能区之前。 有关信息，请参阅[设置变成只读属性](#SettingReadOnlyProperties)。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

 此功能区对象模型主要包含[功能区类](#RibbonClass)、[功能区事件](#RibbonEvents)和[功能区控件类](#RibbonControlClasses)。

## <a name="RibbonClass"></a>功能区类
 将新的 "**功能区（可视化设计器）** " 项添加到项目时，Visual Studio 会将**功能区**类添加到项目。 **功能区**类从<xref:Microsoft.Office.Tools.Ribbon.RibbonBase>类继承。

 此类显示为在功能区代码文件和功能区设计器代码文件之间拆分的分部类。

## <a name="RibbonEvents"></a>功能区事件
 **功能区**类包含以下三个事件：

|事件|描述|
|-----------|-----------------|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.Load>|当 Office 应用程序加载功能区自定义项时引发。 此<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.Load>事件处理程序将自动添加到功能区代码文件中。 此事件处理程序用于在功能区加载时运行自定义代码。|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.LoadImage>|使您能够在功能区加载时缓存功能区自定义项中的图像。 如果在此事件处理程序中编写代码来缓存功能区图像，则可以获得略微的性能提升。 有关详细信息，请参阅 <xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.LoadImage> 。|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.Close>|在功能区实例关闭时引发。|

## <a name="RibbonControlClasses"></a>功能区控件
 命名空间包含在 "工具箱" 的 " **Office 功能区控件**" 组中看到的每个控件的类型。 <xref:Microsoft.Office.Tools.Ribbon>

 下表显示每个`Ribbon`控件的类型。 有关每个控件的说明，请参阅[功能区概述](../vsto/ribbon-overview.md)。

|控件名称|类名|
|------------------|----------------|
|**Box**|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>|
|**Button**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton>|
|**ButtonGroup**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButtonGroup>|
|**CheckBox**|<xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox>|
|**组合框**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>|
|**DropDown**|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>|
|**EditBox**|<xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|
|**库**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**组**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|
|**标签**|<xref:Microsoft.Office.Tools.Ribbon.RibbonLabel>|
|**菜单**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|
|**分隔符**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|
|**SplitButton**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|
|Tab|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|
|**ToggleButton**|<xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|

 命名空间对这些类型使用 "功能区" 前缀，以避免名称与<xref:System.Windows.Forms>命名空间中的控件类的名称冲突。 <xref:Microsoft.Office.Tools.Ribbon>

 向功能区设计器添加控件时，功能区设计器会将该控件的类声明为功能区设计器代码文件中的字段。

### <a name="common-tasks-using-the-properties-of-ribbon-controls"></a>使用功能区控件的属性的常见任务
 每`Ribbon`个控件都包含可用于执行各种任务的属性，例如向控件分配标签或隐藏和显示控件。

 在某些情况下，属性将在功能区加载后或控件添加到动态菜单之后变为只读。 有关详细信息，请参阅[设置变成只读属性](#SettingReadOnlyProperties)。

 下表介绍了一些可以通过使用`Ribbon`控件属性执行的任务。

|对于此任务：|执行此操作：|
|--------------------|--------------|
|隐藏或显示控件。|使用 Visible 属性。|
|启用或禁用控件。|使用 "已启用" 属性。|
|设置控件的大小。|使用 ControlSize 属性。|
|获取显示在控件上的图像。|使用 Image 属性。|
|更改控件的标签。|使用 "标签" 属性。|
|向控件添加用户定义数据。|使用 Tag 属性。|
|获取<xref:Microsoft.Office.Tools.Ribbon.RibbonBox> 、<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>、或中的项<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>控件.|使用 Items 属性。|
|向<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>、 <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>或控件添加项。<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|使用 Items 属性。|
|向添加控件<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>。|使用 Items 属性。<br /><br /> 若要在功能区<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>加载到 office 应用程序中之后将控件添加到中，则<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.Dynamic%2A>必须在功能区加载到 office 应用程序中之前将属性设置为**true** 。 有关信息，请参阅[设置变成只读属性](#SettingReadOnlyProperties)。|
|获取的选定项<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>，<br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> 或 <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>.|使用 SelectedItem 属性。 对于，请使用<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.Text%2A>属性。 <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>|
|获取上<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>的组。|使用 <xref:Microsoft.Office.Tools.Ribbon.RibbonTab.Groups%2A> 属性。|
|指定在中<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>显示的行数和列数。|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.RowCount%2A>使用和<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ColumnCount%2A>属性。|

## <a name="SettingReadOnlyProperties"></a>设置变成只读属性
 某些属性只能在功能区加载之前设置。 设置这些属性有三个位置：

- 在 Visual Studio 的 "**属性**" 窗口中。

- 在**功能区**类的构造函数中。

- 在项目的`ThisAddin`、 `ThisWorkbook`或`CreateRibbonExtensibilityObject` 类`ThisDocument`的方法中。

  动态菜单提供一些例外。 你可以创建新的控件，设置其属性，然后在运行时将它们添加到动态菜单，即使在包含该菜单的功能区加载后也是如此。

  可随时设置添加到动态菜单的控件的属性。

  有关详细信息，请参阅[变成只读属性](#ReadOnlyProperties)。

### <a name="set-properties-in-the-constructor-of-the-ribbon"></a>在功能区的构造函数中设置属性
 可以在**功能区**类的构造`Ribbon`函数中设置控件的属性。 此代码必须在调用`InitializeComponent`方法后出现。 下面的示例在当前时间为17:00 太平洋时间（UTC-8）或更晚时向组中添加一个新按钮。

 添加以下代码。

 [!code-csharp[Trin_Ribbon_ObjectModel#1](../vsto/codesnippet/CSharp/trin_Ribbon_objectmodel_dotnet4/Ribbon1.Designer.cs#1)]
 [!code-vb[Trin_Ribbon_ObjectModel#1](../vsto/codesnippet/VisualBasic/trin_Ribbon_objectmodel_dotnet4/Ribbon1.Designer.vb#1)]

 在从C# visual Studio 2008 升级的 visual 项目中，该构造函数将出现在功能区代码文件中。

 在 Visual Basic 项目或在中C# [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)]创建的 Visual 项目中，构造函数将显示在功能区设计器代码文件中。 此文件名为*YourRibbonItem*。Designer.cs 或*YourRibbonItem*。设计器 .vb。 若要在 Visual Basic 项目中查看此文件，必须先单击解决方案资源管理器中的 "**显示所有文件**" 按钮。

### <a name="set-properties-in-the-createribbonextensibilityobject-method"></a>在 CreateRibbonExtensibilityObject 方法中设置属性
 当你在项目的`Ribbon` `ThisAddin` `CreateRibbonExtensibilityObject` 、 `ThisWorkbook`或类中重写方法时，可以设置控件的属性。`ThisDocument` 有关`CreateRibbonExtensibilityObject`方法的详细信息，请参阅[功能区概述](../vsto/ribbon-overview.md)。

 下面的示例在 Excel 工作簿项目`CreateRibbonExtensibilityObject`的`ThisWorkbook`类的方法中设置功能区属性。

 添加以下代码。

 [!code-vb[Trin_Ribbon_ObjectModel#2](../vsto/codesnippet/VisualBasic/trin_Ribbon_objectmodel_dotnet4/ThisWorkbook.vb#2)]
 [!code-csharp[Trin_Ribbon_ObjectModel#2](../vsto/codesnippet/CSharp/trin_Ribbon_objectmodel_dotnet4/ThisWorkbook.cs#2)]

### <a name="ReadOnlyProperties"></a>变为只读的属性
 下表显示了只可在功能区加载之前设置的属性。

> [!NOTE]
> 你可以随时在动态菜单上设置控件的属性。 此表不适用于这种情况。

|属性|功能区控件类|
|--------------|--------------------------|
|**BoxStyle**|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>|
|**ButtonType**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|
|**ColumnCount**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ControlId**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|
|**DialogLauncher**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|
|**动态**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|
|**Global**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**组合**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|
|**ImageName**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDialogLauncher><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|
|**ItemSize**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|
|**MaxLength**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|
|**Name**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComponent>|
|**置于**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGroup><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonTab><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|
|**RibbonType**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**RowCount**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ShowItemImage**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ShowItemLabel**|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ShowItemSelection**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**SizeString**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|
|**StartFromScratch**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**选项卡**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**标题**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|

### <a name="set-properties-for-ribbons-that-appear-in-outlook-inspectors"></a>为显示在 Outlook 检查器中的功能区设置属性
 每次用户打开出现功能区的检查器时，都会创建功能区的新实例。 但是，您只能在创建功能区的第一个实例之前，设置上表中列出的属性。 在创建第一个实例之后，这些属性将变为只读，因为第一个实例定义 Outlook 用于加载功能区的 XML 文件。

 如果在创建功能区的其他实例时有条件逻辑将这些属性设置为不同的值，则此代码将不起作用。

> [!NOTE]
> 确保为添加到 Outlook 功能区的每个控件设置**名称**属性。 如果在运行时将控件添加到 Outlook 功能区，则必须在代码中设置此属性。 如果在设计时将控件添加到 Outlook 功能区，则会自动设置 "名称" 属性。

## <a name="ribbon-control-events"></a>功能区控件事件
 每个控件类都包含一个或多个事件。 下表描述了这些事件。

|事件|描述|
|-----------|-----------------|
|单击|在单击控件时发生。|
|TextChanged|当编辑框或组合框的文本更改时发生。|
|ItemsLoading|在 Office 请求控件的项集合时发生。 Office 将缓存 Items 集合，直到代码更改控件的属性或调用<xref:Microsoft.Office.Core.IRibbonUI.InvalidateControl%2A>方法。|
|ButtonClick|当单击<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>或<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>中的按钮时发生。|
|SelectionChanged|当中<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>的所选内容更改时发生。|
|DialogLauncherClick|在单击组右下角的对话框启动器图标时发生。|

 这些事件的事件处理程序具有以下两个参数。

|参数|描述|
|---------------|-----------------|
|*sender*|一个<xref:System.Object> ，它表示引发事件的控件。|
|*e*|<xref:Microsoft.Office.Tools.Ribbon.RibbonControlEventArgs> 一个<xref:Microsoft.Office.Core.IRibbonControl>包含的。 使用此控件可访问提供[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]的功能区对象模型中不可用的任何属性。|

## <a name="see-also"></a>请参阅
- [在运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)
- [功能区概述](../vsto/ribbon-overview.md)
- [如何：自定义功能区入门](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [演练：在运行时更新功能区上的控件](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)
- [自定义 Outlook 功能区](../vsto/customizing-a-ribbon-for-outlook.md)
- [如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)
- [如何：向 Backstage 视图添加控件](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [如何：将功能区从功能区设计器导出到功能区 XML](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [如何：显示外接程序用户界面错误](../vsto/how-to-show-add-in-user-interface-errors.md)
