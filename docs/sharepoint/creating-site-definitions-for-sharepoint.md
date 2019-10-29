---
title: 为 SharePoint 创建网站定义 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, site definitions
- site definitions [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5a75b7143412d360a7663e7cf94a1244d66d15a2
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72984528"
---
# <a name="create-site-definitions-for-sharepoint"></a>为 SharePoint 创建网站定义
  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的 SharePoint 站点定义项目允许您创建一个*站点定义，该站点定义*用作新 SharePoint 站点的基础。 这些定义不仅确定了 SharePoint 站点的外观和行为，还决定了其默认内容和功能。 在定义中，可以放置预配置的列表、内容类型、事件接收器、图像和其他项。 例如 SharePoint 包含某些网站定义（如 BLOG）。 基于博客网站定义创建网站时，该站点包含博客网站所需的列表、Web 部件和其他项。

 有关站点定义的详细信息，请参阅[站点模板和定义](/previous-versions/office/developer/sharepoint-2010/ms434313(v=office.14))。

## <a name="site-definition-projects"></a>网站定义项目
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的站点定义项目仅提供 SharePoint 站点所需的基本文件;它们不提供任何默认功能。 必须添加文件和内容才能提供所需的功能。 您可以通过创建和添加所需的文件，手动生成站点。

## <a name="feature-stapling"></a>功能装订
 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中创建站点定义的一个优点是它们会自动使用*功能装订*。 功能装订将功能附加到站点定义，而不是将其功能嵌入到站点定义本身中。 这样，便可以将功能添加到使用站点定义创建的任何站点，而无需修改原始站点定义。 有关详细信息，请参阅[功能装订](/previous-versions/office/developer/sharepoint-2007/bb861862(v=office.12))。

## <a name="site-definition-project-components"></a>网站定义项目组件
 创建站点定义解决方案时，会将以下默认文件添加到其**SiteDefinition**节点。

|文件名|描述|
|---------------|-----------------|
|*default.aspx*|新的 SharePoint 站点的默认 ASPX 主页。|
|*onet.xml*|指定新站点的配置、站点定义模板的组件和默认行为。 这些设置可以包含属性，如已启用的内容类型、默认列表视图、文档模板文件以及站点中包含的 Web 部件。 默认情况下，"`Modules`" 部分列出了要添加到 SharePoint 站点的文件以及如何对其进行配置。|
|*webtemp_\<SiteDefinitionName > .xml*|指定在 "**新建 SharePoint 网站**" 页的 "**模板选择**" 部分中显示的站点定义配置。|

 默认情况下，所有站点定义都存储在*\<驱动器： > \Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\TEMPLATE\SiteTemplates*文件夹中。 每个网站定义都有其自己的子文件夹。

## <a name="related-topics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[演练：创建基本站点定义项目](../sharepoint/walkthrough-create-a-basic-site-definition-project.md)|逐步引导你在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中创建基本网站定义项目。|
|[如何：创建自定义站点定义和配置](/previous-versions/office/developer/sharepoint-2010/ms454677(v=office.14))|介绍如何通过复制现有网站定义，然后修改副本，在 SharePoint 中创建自定义网站定义。|
|[*WebTemp*](/previous-versions/office/developer/sharepoint-2010/ms447717(v=office.14))|描述指定在 "**新建 SharePoint 网站**" 页的 "**模板选择**" 部分中可用的站点定义的原始文件。|
|[本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)|描述如何准备用于全局使用的 SharePoint 解决方案。|
|[为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)|介绍如何创建用户可修改的 SharePoint 页面部分。|
|[为 web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)|介绍如何创建在应用程序页中运行和 Web 部件的可重用控件。|
|[Visual Web Developer](/previous-versions/visualstudio/visual-studio-2010/ms178093(v=vs.100))|介绍如何使用在项目中打开网页时显示的设计器。|
|[ASP.NET 网页概述](/previous-versions/aspnet/428509ah(v=vs.100))|提供有关 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 网页结构、[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]如何处理页面以及 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 页面如何显示符合 XHTML 标准的标记的一般信息。|
|[ASP.NET 网页语法](/previous-versions/aspnet/k33801s3(v=vs.100))|描述构成 ASP.NET 页面的标记元素。|
|[编程 ASP.NET 网页](/previous-versions/aspnet/0yt4zca8(v=vs.100))|提供有关如何在 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 页面中创建事件处理程序以及如何使用客户端脚本的信息。|
|[Windows SharePoint Services 中的编程](/previous-versions/office/developer/sharepoint-services/ms430674(v=office.12))|介绍如何使用中提供的托管对象模型 [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)]。|

## <a name="see-also"></a>请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
