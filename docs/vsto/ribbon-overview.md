---
title: 功能区概述
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- customizing the Ribbon, multiple Ribbons
- Ribbon [Office development in Visual Studio], about Ribbon
- toolbars [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], multiple Ribbons
- toolbars [Office development in Visual Studio]
- custom Ribbon, multiple Ribbons
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5067a52fb9d6a0b6d8991b68a2fce8cdbae987c9
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255943"
---
# <a name="ribbon-overview"></a>功能区概述
  功能区是一种组织相关命令的方式，以便更易于查找。 命令显示为功能区上的控件。 控件在应用程序窗口的上边缘沿水平条带化到各个*组*。 在选项卡上，相关组进行了整理。

 现在可以使用功能区访问在 Microsoft Office 系统早期版本中使用菜单和工具栏访问的大多数功能。 有关详细信息，请参阅技术文章[2007 Microsoft Office 系统用户界面的开发人员概述](http://go.microsoft.com/fwlink/?LinkID=70860)。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

## <a name="customize-the-microsoft-office-ribbon"></a>自定义 Microsoft Office 功能区
 若要自定义功能区，请将以下功能区项之一添加到 Office 项目：

- **功能区（可视化设计器）**

- **功能区（XML）**

  例如，若要自定义 Excel 功能区，则将功能区项添加到 Excel VSTO 外接程序项目中。

### <a name="ribbon-visual-designer-item"></a>功能区（可视化设计器）项
 "**功能区（可视化设计器）** " 项提供了高级工具，使您可以更轻松地设计和开发自定义功能区。 使用 "**功能区（可视化设计器）** " 项可通过以下方式自定义功能区：

- 向功能区添加自定义选项卡或内置选项卡。

- 将自定义组添加到自定义或内置选项卡。

  > [!NOTE]
  > 内置选项卡或组是 Microsoft Office 应用程序的功能区上已存在的选项卡或组。 例如，"**数据**" 选项卡是 Excel 中的内置选项卡。 "**连接**" 组是 "**数据**" 选项卡上的内置组。

- 将自定义控件添加到自定义组。

- 将自定义控件添加到 Backstage 视图。

  有关如何使用 "**功能区（可视化设计器）** " 项自定义功能区的详细信息，请参阅[功能区设计器](../vsto/ribbon-designer.md)。

### <a name="ribbon-xml-item"></a>功能区（XML）项
 如果要以**功能区（可视化设计器）** 项不支持的方式自定义功能区，请使用 "**功能区（XML）** " 项。 使用 "**功能区（XML）** " 项可通过以下方式自定义功能区：

- 将*内置*组添加到自定义选项卡或内置选项卡。

- 将内置控件添加到自定义组。

- 添加自定义代码，以替代内置控件的事件处理程序。

- 自定义“快速访问工具栏”。

- 通过使用限定 ID，在 VSTO 外接程序之间共享功能区自定义项。

  有关如何使用 "**功能区（XML）** " 项自定义功能区的详细信息，请参阅[功能区 XML](../vsto/ribbon-xml.md)。

## <a name="export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml"></a>将功能区从功能区设计器导出到功能区 XML
 如果使用功能区设计器创建功能区，然后决定要以**功能区（可视化设计器）** 项不支持的方式自定义功能区，则可以将功能区导出到 XML。

 Visual Studio 会自动创建一个**功能区（XML）** 项，并使用功能区上的每个控件的元素和特性填充功能区 XML 文件。

 并非功能区设计器的 "**属性**" 窗口中的所有属性都将传输到功能区 XML 文件。  例如，Visual Studio 不会导出**Image**或**Text**属性的值。 这是因为你必须在导出项目的功能区代码文件中创建一个回调方法，以分配图像或设置控件的文本。 在导出过程中，Visual Studio 不会自动生成回调方法。

 此外，任何未更改的默认属性值都不会出现在生成的功能区 XML 文件中。

 有关如何将功能区导出到 XML 的详细信息，请[参阅如何：将功能区从功能区设计器导出到](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)功能区 XML。

### <a name="update-the-code"></a>更新代码
 新的功能区代码文件将添加到**解决方案资源管理器**。 此文件包含功能区 XML 类。 必须在此类的 `Ribbon Callbacks` 区域中创建回调方法，以处理用户操作（例如单击某个按钮）。 将你的代码从事件处理程序移动到这些回调方法，并修改此代码以使用功能区扩展性 (RibbonX) 编程模型。 有关更多信息，请参见 [Ribbon XML](../vsto/ribbon-xml.md)。

 还必须将代码添加到替代 `CreateRibbonExtensibilityObject` 方法并将功能区 XML 类返回到 Office 应用程序的 `ThisAddIn`、`ThisWorkbook` 或 `ThisDocument` 类。

 有关更多信息，请参见 [Ribbon XML](../vsto/ribbon-xml.md)。

## <a name="add-multiple-ribbon-items-to-a-project"></a>向项目添加多个功能区项
 可以将多个功能区项添加到单个项目中。 如果想要执行以下两项任务之一，这会非常有用：

- 创建 Outlook*检查*器的功能区。 有关详细信息，请参阅[自定义 Outlook 功能区](../vsto/customizing-a-ribbon-for-outlook.md)。

    > [!NOTE]
    > 检查器是当用户执行某些任务时（例如，创建一封电子邮件时）打开的窗口。

- 选择要在运行时显示的功能区。

### <a name="select-which-ribbons-to-display-at-run-time"></a>选择要在运行时显示的功能区
 由于一个项目可以包含多个功能区，因此你可以选择要在运行时显示的功能区。

 若要选择要在运行时显示的功能区， `CreateRibbonExtensibilityObject`请重写`ThisAddin`项目`ThisWorkbook`的、 `ThisDocument`或类中的方法，并返回要显示的功能区。 下面的示例检查名为`myCondition`的字段的值，并返回相应的功能区。

> [!NOTE]
> 本示例中使用的语法返回使用 "**功能区（可视化设计器）** " 项创建的功能区。 返回使用**功能区（XML）** 项创建的功能区的语法略有不同。 有关返回**功能区（XML）** 项的详细信息，请参阅[功能区 XML](../vsto/ribbon-xml.md)。

 添加以下代码：

 [!code-vb[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/VisualBasic/trin_Ribbon_choose_Ribbon_4/ThisWorkbook.vb#1)]
 [!code-csharp[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/CSharp/trin_Ribbon_choose_Ribbon_4/ThisWorkbook.cs#1)]

### <a name="related-topics"></a>相关主题

|标题|说明|
|-----------|-----------------|
|[如何：自定义功能区入门](../vsto/how-to-get-started-customizing-the-ribbon.md)|演示如何自定义 Microsoft Office 应用程序的功能区、向 Office 项目添加**功能区（可视化设计器）** 或**功能区（XML）** 项。|
|[功能区设计器](../vsto/ribbon-designer.md)|介绍如何使用功能区设计器将自定义选项卡、组和控件添加到 Microsoft Office 应用程序的功能区。|
|[演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)|显示如何通过使用功能区设计器创建自定义功能区选项卡。 可使用功能区设计器将控件添加和放置到自定义选项卡上。|
|[功能区对象模型概述](../vsto/ribbon-object-model-overview.md)|提供了强类型对象模型的概述，该模型可用于在运行时获取和设置功能区控件的属性。|
|[演练：在运行时更新功能区上的控件](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)|演示如何使用功能区对象模型在功能区加载到 Office 应用程序之后，更新该功能区上的控件。|
|[自定义 Outlook 功能区](../vsto/customizing-a-ribbon-for-outlook.md)|提供用于在 Microsoft Office Outlook 中自定义功能区的指南。|
|[自定义 InfoPath 功能区](../vsto/customizing-a-ribbon-for-infopath.md)|提供用于在 Microsoft Office InfoPath 中自定义功能区的指南。|
|[在运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)|演示如何显示、隐藏和修改功能区，并使用户能够从自定义任务窗格、操作窗格或 Outlook 窗体区域中的控件运行代码。|
|[如何：更改功能区上选项卡的位置](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)|演示如何更改功能区上选项卡的顺序。|
|[如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)|显示如何将组和控件添加到内置选项卡。|
|[如何：向 Backstage 视图添加控件](../vsto/how-to-add-controls-to-the-backstage-view.md)|演示如何将控件添加到单击**文件**时打开的菜单。|
|[如何：向功能区组添加对话框启动器](../vsto/how-to-add-a-dialog-box-launcher-to-a-ribbon-group.md)|说明如何向功能区上的任何组添加对话框启动器。|
|[如何：将功能区从功能区设计器导出到功能区 XML](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)|演示如何通过将功能区从设计器导出到功能区 XML，以高级方式自定义功能区。|
|[Ribbon XML](../vsto/ribbon-xml.md)|介绍如何使用功能区 XML 自定义功能区。|
|[演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)|演示如何使用 "**功能区（XML）** " 项创建自定义功能区选项卡。|
