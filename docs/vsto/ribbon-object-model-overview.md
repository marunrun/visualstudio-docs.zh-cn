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
ms.openlocfilehash: 83f906ad9e5ded349250fe5324076527975c9bf6
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446995"
---
# <a name="ribbon-object-model-overview"></a>功能区对象模型概述
  [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]公开可用于获取和设置在运行时的功能区控件的属性的强类型化的对象模型。 例如，您可以动态填充菜单控件，或显示和隐藏控件根据上下文。 向功能区，但只能在功能区加载 Office 应用程序之前，还可以添加选项卡、 组和控件。 有关信息，请参阅[设置属性变为只读](#SettingReadOnlyProperties)。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

 此功能区对象模型包含主要[功能区类](#RibbonClass)，[功能区事件](#RibbonEvents)，并[功能区控件类](#RibbonControlClasses)。

## <a name="RibbonClass"></a> 功能区类
 添加一个新**功能区 （可视化设计器）** Visual Studio 将添加到项目，项**功能区**类到你的项目。 **功能区**类继承自<xref:Microsoft.Office.Tools.Ribbon.RibbonBase>类。

 此类显示为功能区代码文件和功能区设计器代码文件之间拆分的分部类。

## <a name="RibbonEvents"></a> 功能区事件
 **功能区**类包含以下三个事件：

|Event|描述|
|-----------|-----------------|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.Load>|当 Office 应用程序加载功能区自定义项时引发。 <xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.Load>事件处理程序会自动添加到功能区代码文件。 使用此事件处理程序运行时在功能区加载自定义代码。|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.LoadImage>|您可以在功能区自定义项的缓存映像时在功能区加载。 如果您编写代码以缓存此事件处理程序中的功能区映像，可以获取略微的性能提升。 有关详细信息，请参阅 <xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.LoadImage>。|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.Close>|功能区实例关闭时引发。|

## <a name="RibbonControlClasses"></a> 功能区控件
 <xref:Microsoft.Office.Tools.Ribbon>命名空间包含您在中看到每个控件的类型**Office 功能区控件**组**工具箱**。

 下表显示每个类型`Ribbon`控件。 每个控件的说明，请参阅[功能区概述](../vsto/ribbon-overview.md)。

|控件名称|类名|
|------------------|----------------|
|**Box**|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>|
|**Button**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton>|
|**ButtonGroup**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButtonGroup>|
|**CheckBox**|<xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox>|
|**组合框**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>|
|**DropDown**|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>|
|**EditBox**|<xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|
|**Gallery**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**组**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|
|**标签**|<xref:Microsoft.Office.Tools.Ribbon.RibbonLabel>|
|**菜单**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|
|**分隔符**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|
|**SplitButton**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|
|Tab|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|
|**ToggleButton**|<xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|

 <xref:Microsoft.Office.Tools.Ribbon>命名空间使用这些类型的"功能区"前缀以避免名称冲突，名称中的控件类<xref:System.Windows.Forms>命名空间。

 当将控件添加到功能区设计器时，功能区设计器将为该控件类声明为功能区设计器代码文件中的字段。

### <a name="common-tasks-using-the-properties-of-ribbon-controls"></a>使用功能区控件的属性的常见任务
 每个`Ribbon`控件包含可用于执行各种任务，如将标签分配到一个控件，或隐藏和显示控件的属性。

 在某些情况下，属性变为只读后加载功能区或控件添加到动态菜单。 有关详细信息，请参阅[设置属性变为只读](#SettingReadOnlyProperties)。

 下表介绍了一些可以使用执行的任务`Ribbon`控件属性。

|对于此任务：|执行此操作：|
|--------------------|--------------|
|隐藏或显示控件。|使用可见的属性。|
|启用或禁用控件。|使用已启用属性。|
|设置控件的大小。|使用 ControlSize 属性。|
|获取在控件显示的图像。|使用图像属性。|
|更改控件的标签。|使用标签属性。|
|向控件添加用户定义的数据。|使用 Tag 属性。|
|获取中的项<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>， <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>， <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>，或<br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton> 控件。|使用项目属性。|
|将项添加到<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>， <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>，或<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>控件。|使用项目属性。|
|将控件添加到<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>。|使用项目属性。<br /><br /> 若要将控件添加到<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>功能区加载到 Office 应用程序后，必须设置<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.Dynamic%2A>属性设置为**true**功能区加载到 Office 应用程序之前。 有关信息，请参阅[设置属性变为只读](#SettingReadOnlyProperties)。|
|获取选定的项的<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>，<br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>或<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>。|使用 SelectedItem 属性。 有关<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>，使用<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.Text%2A>属性。|
|获取组<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>。|使用 <xref:Microsoft.Office.Tools.Ribbon.RibbonTab.Groups%2A> 属性。|
|指定行和列中显示的数字<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>。|使用<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.RowCount%2A>和<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ColumnCount%2A>属性。|

## <a name="SettingReadOnlyProperties"></a> 设置变为只读的属性
 某些属性仅在功能区加载之前设置。 有以下三个位置设置这些属性：

- 在 Visual Studio**属性**窗口。

- 中的构造函数**功能区**类。

- 在中`CreateRibbonExtensibilityObject`方法`ThisAddin`， `ThisWorkbook`，或`ThisDocument`你的项目的类。

  动态菜单提供了一些例外情况。 可以创建新控件、 设置其属性，然后甚至加载包含该菜单在功能区后，会将它们添加到在运行时，动态菜单。

  可以随时设置添加到动态菜单的控件的属性。

  有关详细信息，请参阅[变为只读属性](#ReadOnlyProperties)。

### <a name="set-properties-in-the-constructor-of-the-ribbon"></a>在功能区的构造函数中设置属性
 可以设置的属性`Ribbon`的构造函数中的控件**功能区**类。 此代码必须在调用后出现`InitializeComponent`方法。 下面的示例向组添加一个新按钮，如果当前时间为 17:00 太平洋时间 (UTC-8) 或更高版本。

 添加以下代码。

 [!code-csharp[Trin_Ribbon_ObjectModel#1](../vsto/codesnippet/CSharp/trin_Ribbon_objectmodel_dotnet4/Ribbon1.Designer.cs#1)]
 [!code-vb[Trin_Ribbon_ObjectModel#1](../vsto/codesnippet/VisualBasic/trin_Ribbon_objectmodel_dotnet4/Ribbon1.Designer.vb#1)]

 视觉对象中C#从 Visual Studio 2008 升级的项目，该构造函数出现在功能区代码文件中。

 在 Visual Basic 项目中，或在视觉对象C#中创建的项目[!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)]，该构造函数出现在功能区设计器代码文件中。 此文件命名为*YourRibbonItem*。Designer.cs 或*YourRibbonItem*。Designer.vb。 若要查看此文件在 Visual Basic 项目，必须先单击**显示所有文件**在解决方案资源管理器中的按钮。

### <a name="set-properties-in-the-createribbonextensibilityobject-method"></a>CreateRibbonExtensibilityObject 方法中设置属性
 可以设置的属性`Ribbon`控制当重写`CreateRibbonExtensibilityObject`中的方法`ThisAddin`， `ThisWorkbook`，或`ThisDocument`你的项目的类。 有关详细信息`CreateRibbonExtensibilityObject`方法，请参阅[功能区概述](../vsto/ribbon-overview.md)。

 下面的示例设置功能区属性`CreateRibbonExtensibilityObject`方法的`ThisWorkbook`的 Excel 工作簿项目的类。

 添加以下代码。

 [!code-vb[Trin_Ribbon_ObjectModel#2](../vsto/codesnippet/VisualBasic/trin_Ribbon_objectmodel_dotnet4/ThisWorkbook.vb#2)]
 [!code-csharp[Trin_Ribbon_ObjectModel#2](../vsto/codesnippet/CSharp/trin_Ribbon_objectmodel_dotnet4/ThisWorkbook.cs#2)]

### <a name="ReadOnlyProperties"></a> 变为只读的属性
 下表显示只能在功能区加载之前设置的属性。

> [!NOTE]
> 在任何时候，可以设置动态菜单上的控件的属性。 此表不适用于这种情况下。

|属性|功能区控件类|
|--------------|--------------------------|
|**BoxStyle**|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>|
|**ButtonType**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|
|**ColumnCount**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ControlId**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|
|**DialogLauncher**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|
|**Dynamic**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|
|**Global**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**组**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|
|**ImageName**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDialogLauncher><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|
|**ItemSize**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|
|**MaxLength**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|
|**名称**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComponent>|
|**位置**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGroup><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonTab><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|
|**RibbonType**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**RowCount**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ShowItemImage**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ShowItemLabel**|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ShowItemSelection**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**SizeString**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|
|**StartFromScratch**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**Tabs**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**标题**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|

### <a name="set-properties-for-ribbons-that-appear-in-outlook-inspectors"></a>在 Outlook 检查器中设置属性的显示功能区
 每当用户打开功能区将显示的检查器都会创建功能区的新实例。 但是，可以设置仅在创建功能区的第一个实例之前上, 表中列出的属性。 第一个实例创建后，这些属性成为只读的因为第一个实例定义了 Outlook 用于加载功能区 XML 文件。

 如果有任何这些属性设置为不同的值时创建功能区的其他实例的条件逻辑，此代码不会影响。

> [!NOTE]
> 絋粄**名称**属性设置为向 Outlook 功能区添加每个控件。 如果向 Outlook 功能区在运行时添加控件，则必须在代码中设置此属性。 如果在设计时将控件添加到 Outlook 功能区中，会自动设置 Name 属性。

## <a name="ribbon-control-events"></a>功能区控件事件
 每个控件类包含一个或多个事件。 下表描述了这些事件。

|Event|描述|
|-----------|-----------------|
|单击|当单击控件时发生。|
|TextChanged|当编辑框或组合框的文本更改时发生。|
|ItemsLoading|当控件的项集合请求通过 Office 时发生。 Office 缓存的项集合中，直到你的代码更改该控件的属性或调用<xref:Microsoft.Office.Core.IRibbonUI.InvalidateControl%2A>方法。|
|ButtonClick|中的按钮时发生<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>或<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>单击。|
|SelectionChanged|发生时中的选定<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>或<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>更改。|
|DialogLauncherClick|单击右下角的一组对话启动程序时发生。|

 这些事件的事件处理程序具有以下两个参数。

|参数|描述|
|---------------|-----------------|
|*sender*|<xref:System.Object>它表示引发事件的控件。|
|*e*|一个<xref:Microsoft.Office.Tools.Ribbon.RibbonControlEventArgs>，其中包含<xref:Microsoft.Office.Core.IRibbonControl>。 使用此控件可访问的任何属性都在提供的功能区对象模型中不可用[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]。|

## <a name="see-also"></a>请参阅
- [在运行时在功能区的访问](../vsto/accessing-the-ribbon-at-run-time.md)
- [功能区概述](../vsto/ribbon-overview.md)
- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [演练：更新在运行时功能区上的控件](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)
- [为 Outlook 中自定义功能区](../vsto/customizing-a-ribbon-for-outlook.md)
- [如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)
- [如何：将控件添加到 Backstage 视图](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [如何：将功能区从功能区设计器导出到功能区 XML](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [如何：显示外接程序用户界面错误](../vsto/how-to-show-add-in-user-interface-errors.md)
