---
title: Office UI 自定义
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- menus [Office development in Visual Studio], customizing
- actions panes [Office development in Visual Studio], creating
- WPF [Office development in Visual Studio]
- toolbars [Office development in Visual Studio], customizing
- Office applications [Office development in Visual Studio], UI customization
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e5fd0253c6ca560c58724c8a83e343164b678923
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71254144"
---
# <a name="office-ui-customization"></a>Office UI 自定义
  可以使用 Visual Studio 中的 Office 开发人员工具自定义 Microsoft Office 应用程序的用户界面 (UI)。 本主题介绍自定义的 UI 功能，分为以下几个部分：

- [UI 功能的比较](#Comparison)

- [操作窗格和自定义任务窗格](#Actions)

- [自定义功能区 UI](#Ribbon)

- [Backstage 视图](#Backstage)

- [Outlook 窗体区域](#FormRegion)

- [文档上的控件](#Controls)

- [快捷菜单](#Shortcut)

## <a name="Comparison"></a>UI 功能的比较
 下表比较了 Microsoft Office 项目中可自定义的主要 UI 功能。

|功能|支持的项目类型|支持的 Microsoft Office 应用程序|
|-------------|-----------------------------|---------------------------------------------|
|操作窗格|文档级自定义项|Excel<br /><br /> 字|
|自定义任务窗格|VSTO 外接程序|Excel<br /><br /> [!INCLUDE[InfoPath_15_short](../vsto/includes/infopath-15-short-md.md)]<br /><br /> [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)]<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> 字<br /><br /> Excel|
|自定义功能区 UI|文档级自定义项<br /><br /> VSTO 外接程序|Excel<br /><br /> [!INCLUDE[InfoPath_15_short](../vsto/includes/infopath-15-short-md.md)]<br /><br /> [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)]<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> 项目<br /><br /> 字<br /><br /> Visio|
|Backstage 视图|文档级自定义项<br /><br /> VSTO 外接程序|Excel<br /><br /> [!INCLUDE[InfoPath_15_short](../vsto/includes/infopath-15-short-md.md)]。<br /><br /> [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)]<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> 项目<br /><br /> 字<br /><br /> Visio|
|Outlook 窗体区域|VSTO 外接程序|Outlook|
|文档中的控件|文档级自定义项<br /><br /> VSTO 外接程序|Excel<br /><br /> 字|
|快捷菜单|文档级自定义项<br /><br /> VSTO 外接程序|Excel<br /><br /> [!INCLUDE[InfoPath_15_short](../vsto/includes/infopath-15-short-md.md)]<br /><br /> [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)]<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> 项目<br /><br /> 字<br /><br /> Visio<br /><br /> Excel|

## <a name="Actions"></a>操作窗格和自定义任务窗格
 任务窗格是一个用户界面面板，通常停靠在 Microsoft Office 应用程序中某一窗口的一侧。 几乎所有 Microsoft Office 应用程序都包括内置任务窗格。 Word 中的“帮助”任务窗格就是任务窗格的一个示例。

 Visual Studio 中的 Office 开发工具提供了两种不同的自定义任务窗格方法：

- 可以向文档级自定义项添加操作窗格。 默认情况下，操作窗格显示在应用程序的右边，在文档的右侧。 但是，也可以在文档的左侧、顶部或底部显示操作窗格。

- 可以向 VSTO 外接程序添加自定义任务窗格。 用户可以将自定义任务窗格停靠到应用程序窗口中的各侧，也可将自定义任务窗格拖动到窗口中的任意位置。

  操作窗格和自定义任务窗格通过承载各种控件来提供功能，以协助用户进行数据输入等任务。 与功能区组相比，操作窗格和自定义任务窗格提供更大的区域来包括文本和控件。

  有关操作窗格的详细信息，请参阅[操作窗格概述](../vsto/actions-pane-overview.md)。 有关自定义任务窗格的详细信息，请参阅[自定义任务窗格](../vsto/custom-task-panes.md)。

## <a name="Ribbon"></a>自定义功能区 UI
 可以自定义功能区 UI，以显示在 Office 中添加到应用程序的功能。 功能区是一种以控件形式整理相关命令（便于查找）的方法。 可以创建你自己的功能区选项卡和组，以便用户能够访问解决方案中提供的功能。 之前通过使用 Microsoft Office System 早期版本中的菜单和工具栏访问的大多数功能，现在都可以通过使用功能区进行访问。

 有关详细信息，请参阅[功能区概述](../vsto/ribbon-overview.md)。

## <a name="Backstage"></a>Backstage 视图
 在 Office 应用程序中，单击 "**文件**" 选项卡将打开 Backstage 视图。 Backstage 视图提供的用户界面可将文件级别任务和操作组合到一起，从而代替可通过 2007 Microsoft Office system 中 Microsoft Office 按钮使用的类似功能。 Backstage 视图可通过使用 XML 完全扩展。

 Visual Studio 不提供用于自定义 Backstage 视图的设计器或 API。 但是，如果向 Office 项目添加 "**功能区（XML）** " 项，则可以向功能区 xml 文件添加 XML 以自定义 Backstage 视图。 有关**功能区（XML）** 项的详细信息，请参阅[功能区 XML](../vsto/ribbon-xml.md)。

 有关自定义 Backstage 视图的详细信息，请参阅面向[开发人员的 office 2010 backstage 视图的简介](http://go.microsoft.com/fwlink/?LinkId=182189)和[为开发人员自定义 office 2010 backstage 视图](http://go.microsoft.com/fwlink/?LinkId=182188)。

## <a name="FormRegion"></a>Outlook 窗体区域
 使用窗体区域可向标准 Microsoft Office Outlook 窗体添加自定义功能。 你可以使用额外字段或控件创建可扩展任何现有窗体的窗体区域。 如果使用 Visual Studio 中的 Office 开发工具创建新窗体区域，则在窗体区域上仅可使用 Windows 窗体控件。 如果导入在 Outlook 中设计的窗体区域，则仅可使用本机 Outlook 控件。

 你可以创建占用 Outlook UI 不同区域的窗体区域。 例如，窗体第一页的底部显示相邻窗体区域，每个相邻窗体区域都可折叠。 还可以添加作为完整窗体页显示的单独窗体区域，并且该区域可以显示在任何现有标准窗体或自定义窗体上。

 有关详细信息，请参阅[创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)。

## <a name="Controls"></a>文档上的控件
 可以向 Word 文档和 Excel 工作表添加各种控件。 例如，你可能希望向文档添加日期选取器控件，以便用户可以标准格式输入日期，或者在工作表上设置一个按钮，用于将数据发送到数据库。

 开发 Excel 或 Word 文档级项目时，可以在设计时使用 Visual Studio 设计器向项目中的文档或工作簿添加控件，或在运行时以编程方式添加控件。 开发 Excel 或 Word VSTO 外接程序项目时，可以在运行时以编程方式向任何打开的文档或工作簿添加控件。

 有关详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)和[Office 文档上的 Windows 窗体控件概述](../vsto/windows-forms-controls-on-office-documents-overview.md)。

## <a name="Shortcut"></a>快捷菜单
 在文档或应用程序窗口中右键单击时，将出现一个快捷菜单。 可以设置在发生某事件后显示快捷菜单，例如，当用户右键单击文档、工作簿或主机控件时。 可以向快捷菜单添加大量不同的菜单命令或控件。 使用 XML 创建快捷菜单。 如果向 Office 项目添加 "**功能区（XML）** " 项，则可以向功能区 xml 文件添加 xml 以创建快捷菜单。 有关使用 XML 创建快捷菜单的详细信息，请参阅[如何：将命令添加到快捷](../vsto/how-to-add-commands-to-shortcut-menus.md)菜单。

## <a name="see-also"></a>请参阅
- [功能区概述](../vsto/ribbon-overview.md)
- [Office 文档上的 Windows 窗体控件概述](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [操作窗格概述](../vsto/actions-pane-overview.md)
- [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)
- [自定义任务窗格](../vsto/custom-task-panes.md)
- [在 Office 解决方案中使用 WPF 控件](../vsto/using-wpf-controls-in-office-solutions.md)
- [如何：在功能区上显示 "开发人员" 选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)
- [如何：显示外接程序用户界面错误](../vsto/how-to-show-add-in-user-interface-errors.md)
- [演练：使用 Windows 窗体收集数据](../vsto/walkthrough-collecting-data-using-a-windows-form.md)
