---
title: 为 SharePoint 创建页 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: f58af55b18d7cd6341b779d71da2994875c98a62
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62419878"
---
# <a name="create-pages-for-sharepoint"></a>为 SharePoint 创建页
  您可以创建应用程序页、 网页、 母版页和页面布局的 SharePoint 站点。

 可以在 Visual Studio 中使用模板创建应用程序页。 使用 SharePoint Designer 创建站点页面、 母版页和页面布局。 然后，可以导入 Visual Studio SharePoint 项目中使用它们的这些页。

 此外可以通过使用级联样式表、 ECMAScript 和主题修改的外观和行为的页数。

## <a name="types-of-sharepoint-pages"></a>类型的 SharePoint 页
 下表介绍四种主要类型的 SharePoint 站点包含的页数。

|页类型|描述|
|---------------|-----------------|
|应用程序页|如果你想要包含自定义代码的页或你想要在多个站点之间共享的页，请创建应用程序页。 否则，站点页面可能是最佳选择。|
|网站页面|如果你想要执行以下任务中的任何，创建的网站页面：<br /><br /> -添加到 SharePoint 库的页面。<br />-启用主机功能，例如动态 Web 部件和 Web 部件区域页。<br />-使用户能够通过使用 SharePoint Designer 自定义的页。<br /><br /> 如果你想页后，可以包含自定义代码，不要创建的网站页面。 虽然可以将自定义代码添加到站点页面，在代码停止运行时在用户通过使用 SharePoint Designer 自定义页。|
|主页面|创建主页上，如果你想要定义站点页面的通用结构和应用程序页。|
|页面布局|页面布局是特定于[!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)]，可用于进一步定义站点页面和应用程序页的通用结构。|

 有关每种类型的页的概述，请参阅[构建基块：页面和用户界面](http://go.microsoft.com/fwlink/?LinkID=182095)，并[页上的布局和母版页](http://go.microsoft.com/fwlink/?LinkID=182096)。

## <a name="create-application-pages"></a>创建应用程序页
 可以通过添加在 Visual Studio 中创建应用程序页**应用程序页**向 SharePoint 项目项。 可以将控件添加到页上，，然后通过添加代码来处理控件事件。

 可以在页面的代码文件中设置断点、 启动调试器，和测试本地 SharePoint 站点上的页，而不执行任何其他配置步骤。 有关详细信息，请参阅[for SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)。

## <a name="create-site-pages-master-pages-and-page-layouts"></a>创建站点页面、 母版页和页面布局
 可以使用 SharePoint Designer 来创建站点页面、 母版页和页面布局。 然后，您可以将这些页面导入 Visual Studio。 如果你想要利用的部署或 Visual Studio 中提供的源代码管理功能，导入您的页面。 有关详细信息，请参阅[从现有的 SharePoint 网站导入项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)。

 因为很难将其导入后修改这些页面，应在导入之前设计这些页面。

## <a name="create-cascading-style-sheets-ecmascript-and-themes"></a>创建级联样式表、 ECMAScript 和主题
 Visual Studio 不提供开发级联样式表 (CSS)、 ECMAScript （JavaScript、 JScript） 或 SharePoint 站点的主题文件的模板。 使用 SharePoint SDK 中提供的指南，或使用诸如 SharePoint Designer 之类的工具，可以创建这些文件。

 可以直接将这些文件添加到你的解决方案或将其导入。 在任一情况下，必须创建对于您添加的每个项相应的映射的文件夹。 有关如何创建的映射的文件夹的详细信息，请参阅[如何： 添加和移除映射的文件夹](../sharepoint/how-to-add-and-remove-mapped-folders.md)。

 有关创建级联样式表的详细信息，请参阅[级联样式表类中的使用情况 SharePoint Foundation](http://go.microsoft.com/fwlink/?LinkID=182098)。 有关创建 SharePoint 解决方案的 JavaScript 和 JScript 文件的详细信息，请参阅[设置向上的基本 ASPX 页的 ECMAScript](http://go.microsoft.com/fwlink/?LinkID=182099)。 有关主题的详细信息，请参阅[构建基块：页面和用户界面](http://go.microsoft.com/fwlink/?LinkID=182095)。

## <a name="related-topics"></a>相关主题

|标题|描述|
|-----------|-----------------|
|[为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)|介绍如何添加应用程序页面： *.aspx*与 SharePoint 母版页合并的内容。|
|[如何：创建应用程序页](../sharepoint/how-to-create-an-application-page.md)|演示如何创建在 SharePoint 站点运行的 ASP.NET 页面。|
|[演练：创建 SharePoint 应用程序页](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)|演示如何设计和调试 ASP.NET 网页上的 SharePoint 站点。|
