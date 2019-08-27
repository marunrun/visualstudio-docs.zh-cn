---
title: 创建 SharePoint 站点定义 |Microsoft Docs
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
ms.openlocfilehash: 2abf61bbc960e342a395e9c0ff3395ecde852137
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62580964"
---
# <a name="create-site-definitions-for-sharepoint"></a>创建 SharePoint 站点定义
  中的 SharePoint 站点定义项目[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，可以创建*网站定义*，它可作为新的 SharePoint 站点的基础。 这些定义不仅确定的外观和行为的 SharePoint 站点，但还自己的默认内容和功能。 在定义中，您可以放入预配置的列表、 内容类型、 事件接收器、 图像和其他项。 例如 SharePoint 包含某些网站定义（如 BLOG）。 当创建了基于博客站点定义的网站时，站点将包含列表、 Web 部件和博客网站所需的其他项。

 有关网站定义的详细信息，请参阅[站点模板和定义](http://go.microsoft.com/fwlink/?LinkId=179134)。

## <a name="site-definition-projects"></a>站点定义项目
 站点定义中的项目[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]提供仅 SharePoint 站点所需的基本文件; 它们不提供任何默认功能。 必须添加文件和内容，以提供所需的功能。 您可以通过创建并添加所需的文件，手动构建站点。

## <a name="feature-stapling"></a>功能装订
 创建站点定义中的一个好处[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]是时会自动使用*功能装订*。 功能装订将附加到的站点定义而不是站点定义本身中嵌入其功能的一项功能。 这样做可让您将功能添加到使用而无需修改原始的站点定义站点定义创建的任何站点。 有关详细信息，请参阅[功能装订](http://go.microsoft.com/fwlink/?LinkID=119283)。

## <a name="site-definition-project-components"></a>站点定义项目组件
 创建站点定义解决方案时，将以下默认文件添加到其**SiteDefinition**节点。

|文件名|描述|
|---------------|-----------------|
|*default.aspx*|新的 SharePoint 站点默认 ASPX 主页。|
|*onet.xml*|指定新站点的配置、 站点定义模板，默认行为的组件。 这些设置可以包含的内容类型启用的默认列表视图，文档模板文件，如属性和 Web 部件包含与该站点。 默认情况下，`Modules`部分列出了要添加到 SharePoint 站点，如何配置这些设置的文件。|
|*webtemp_\<SiteDefinitionName>.xml*|指定将出现在站点定义配置**模板选择**一部分**新的 SharePoint 站点**页。|

 默认情况下，所有站点定义都存储在 *\<驱动器： > \Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\TEMPLATE\SiteTemplates*文件夹。 每个站点定义具有自己的子文件夹。

## <a name="related-topics"></a>相关主题

|标题|描述|
|-----------|-----------------|
|[演练：创建基本站点定义项目](../sharepoint/walkthrough-create-a-basic-site-definition-project.md)|逐步引导您完成基本站点定义项目中创建[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。|
|[如何：创建自定义站点定义和配置](http://go.microsoft.com/fwlink/?LinkId=183309)|介绍如何在 SharePoint 中创建自定义网站定义通过复制现有的站点定义和修改该副本。|
|[*WebTemp.xml*](http://go.microsoft.com/fwlink/?LinkId=183310)|描述指定的站点定义中提供的原始文件**模板选择**一部分**新的 SharePoint 站点**页。|
|[本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)|介绍如何准备 SharePoint 解决方案的共用。|
|[为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)|介绍如何创建 SharePoint 页，用户可以修改的部分。|
|[创建 web 部件或应用程序页的可重用的控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)|介绍如何创建在应用程序页和 Web 部件中运行的可重用控件。|
|[Visual Web 开发人员](http://go.microsoft.com/fwlink/?LinkId=178725)|介绍如何使用在项目中打开网页时，将显示在设计器。|
|[ASP.NET 网页概述](http://go.microsoft.com/fwlink/?LinkId=178726)|提供有关结构的常规信息[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]网页，如何通过处理页面[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]，以及如何[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]页显示符合 XHTML 标准的标记。|
|[ASP.NET 网页语法](http://go.microsoft.com/fwlink/?LinkId=178727)|描述组成 ASP.NET 页面的标记元素。|
|[编程的 ASP.NET Web Pages](http://go.microsoft.com/fwlink/?LinkId=178728)|提供有关如何创建事件处理程序中的信息[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]页以及如何使用客户端脚本。|
|[在 Windows SharePoint Services 中编程](http://go.microsoft.com/fwlink/?LinkId=178729)|介绍如何使用中提供的托管的对象模型[!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)]。|

## <a name="see-also"></a>请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
