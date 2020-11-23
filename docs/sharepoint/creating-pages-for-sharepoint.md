---
title: 为 SharePoint 创建页 | Microsoft Docs
description: 使用 Visual Studio 中的模板为 SharePoint 创建应用程序页。 使用 SharePoint Designer 创建网站页、母版页和页面布局。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, master pages
- SharePoint development in Visual Studio, page layouts
- SharePoint development in Visual Studio, content pages
- master pages[SharePoint development in Visual Studio], designing
- content pages[SharePoint development in Visual Studio], designing
- page layouts[SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 974ddb3c68d0c2ef297c884e75300a8507f436cc
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850619"
---
# <a name="create-pages-for-sharepoint"></a>为 SharePoint 创建页
  可为 SharePoint 网站创建应用程序页、网站页、母版页和页面布局。

 可使用 Visual Studio 中的模板创建应用程序页。 使用 SharePoint Designer 创建网站页、母版页和页面布局。 然后，可将这些页面导入到 Visual Studio 中，以便在 SharePoint 项目中使用它们。

 还可通过使用级联样式表、ECMAScript 和主题来修改页面的外观和行为。

## <a name="types-of-sharepoint-pages"></a>SharePoint 页面的类型
 下表介绍了 SharePoint 网站包含的 4 种主要的页面类型。

|页面类型|说明|
|---------------|-----------------|
|应用程序页|如果希望页面包含自定义代码，或者要在多个网站之间共享页面，请创建应用程序页。 否则，网站页可能是最佳选择。|
|网站页|如果要执行以下任一任务，请创建网站页：<br /><br /> - 将页面添加到 SharePoint 库中。<br />- 启用页面以承载动态 Web 部件和 Web 部件区域等功能。<br />- 允许用户使用 SharePoint Designer 自定义页面。<br /><br /> 如果希望页面包含自定义代码，请不要创建网站页。 尽管可向网站页添加自定义代码，但当用户使用 SharePoint Designer 自定义页面时，代码将停止运行。|
|母版页|如果要为网站页和应用程序页定义通用结构，请创建母版页。|
|页面布局|页面布局特定于 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)]，你可用它来进一步定义网站页和应用程序页的通用结构。|

 要概要了解每种类型的页面，请参阅 [构建基块：页面和用户界面](/previous-versions/office/developer/sharepoint-2010/ee539040(v=office.14))和[页面布局和母版页](/previous-versions/office/developer/sharepoint-2010/ms543497(v=office.14))。

## <a name="create-application-pages"></a>创建应用程序页
 可通过向 SharePoint 项目添加“应用程序页”项，在 Visual Studio 中创建应用程序页。 可向页面添加控件，然后添加代码来处理控件事件。

 可在页面的代码文件中设置断点，启动调试程序，并在本地 SharePoint 网站上测试页面，而无需执行任何其他配置步骤。 有关详细信息，请参阅[为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)。

## <a name="create-site-pages-master-pages-and-page-layouts"></a>创建网站页、母版页和页面布局
 可使用 SharePoint Designer 创建网站页、母版页和页面布局。 然后，可将这些页面导入到 Visual Studio 中。 如果要利用 Visual Studio 中提供的部署或源代码管理功能，请导入页面。 有关详细信息，请参阅[从现有的 SharePoint 网站导入项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)。

 由于页面导入后修改起来很困难，因此应在导入前对它们进行设计。

## <a name="create-cascading-style-sheets-ecmascript-and-themes"></a>创建级联样式表、ECMAScript 和主题
 Visual Studio 不提供模板用于为 SharePoint 网站开发级联样式表 (CSS)、ECMAScript (JavaScript/JScript) 或主题文件。 你可使按照 SharePoint SDK 中提供的指南或使用 SharePoint Designer 等工具来创建这些文件。

 可直接将这些文件添加到解决方案中，也可导入它们。 无论如何，都必须为添加的每个项创建适当的映射文件夹。 要详细了解如何创建映射文件夹，请参阅[如何：添加和删除映射文件夹](../sharepoint/how-to-add-and-remove-mapped-folders.md)。

 要详细了解如何创建级联样式表，请参阅[级联样式表类在 SharePoint Foundation 中的用法](/previous-versions/office/developer/sharepoint-2010/ms438349(v=office.14))。 要详细了解如何为 SharePoint 解决方案创建 JavaScript 和 JScript 文件，请参阅[设置 ECMAScript 的基本 ASPX 页](/previous-versions/office/developer/sharepoint-2010/ee535709(v=office.14))。 有关主题的详细信息，请参阅[构建基块：页面和用户界面](/previous-versions/office/developer/sharepoint-2010/ee539040(v=office.14))。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)|介绍如何添加应用程序页（即与 SharePoint 母版页合并的 .aspx 内容）。|
|[如何：创建应用程序页](../sharepoint/how-to-create-an-application-page.md)|介绍如何创建在 SharePoint 网站上运行的 ASP.NET 页面。|
|[演练：创建 SharePoint 应用程序页](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)|介绍如何设计和调试 SharePoint 网站的 ASP.NET 网页。|
