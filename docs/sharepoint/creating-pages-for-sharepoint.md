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
ms.openlocfilehash: 297ebf0e7c2ed1273dd5a8ac973ce497c4c64781
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72986356"
---
# <a name="create-pages-for-sharepoint"></a>创建 SharePoint 页面
  您可以为 SharePoint 站点创建应用程序页、网站页、母版页和页面布局。

 可以使用 Visual Studio 中的模板创建应用程序页。 使用 SharePoint Designer 创建网站页、母版页和页面布局。 然后，可以将这些页面导入到 Visual Studio 中，以便在 SharePoint 项目中使用它们。

 还可以通过使用级联样式表、ECMAScript 和主题来修改页面的外观和行为。

## <a name="types-of-sharepoint-pages"></a>SharePoint 页面的类型
 下表介绍了 SharePoint 站点包含的四种主要类型的页面。

|页面类型|说明|
|---------------|-----------------|
|应用程序页|如果希望页面包含自定义代码或要在多个站点之间共享页面，请创建应用程序页。 否则，站点页可能是最佳选择。|
|网站页面|如果要执行以下任何任务，请创建站点页面：<br /><br /> -将页面添加到 SharePoint 库。<br />-启用页以承载动态 Web 部件和 Web 部件区域等功能。<br />-使用户能够使用 SharePoint Designer 自定义页面。<br /><br /> 如果希望该页包含自定义代码，请不要创建网站页。 虽然您可以将自定义代码添加到站点页，但当用户使用 SharePoint 设计器自定义该页时，代码将停止运行。|
|母版页|如果要为网站页面和应用程序页面定义公共结构，请创建一个母版页。|
|页面布局|页面布局特定于 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)]，并使你能够进一步为网站页面和应用程序页面定义公共结构。|

 有关每种类型的页面的概述，请参阅 [构建基块：页面和用户界面](/previous-versions/office/developer/sharepoint-2010/ee539040(v=office.14))、[页面布局和母版页](/previous-versions/office/developer/sharepoint-2010/ms543497(v=office.14))。

## <a name="create-application-pages"></a>创建应用程序页
 可以通过向 SharePoint 项目添加 "**应用程序页**" 项来在 Visual Studio 中创建应用程序页。 您可以向页中添加控件，然后通过添加代码来处理控件事件。

 您可以在页的代码文件中设置断点，启动调试器，然后在本地 SharePoint 站点上测试页面，而无需执行任何其他配置步骤。 有关详细信息，请参阅[创建 SharePoint 的应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)。

## <a name="create-site-pages-master-pages-and-page-layouts"></a>创建网站页、母版页和页面布局
 您可以使用 SharePoint Designer 创建网站页、母版页和页面布局。 然后，可以将这些页面导入到 Visual Studio 中。 如果要利用 Visual Studio 中提供的部署或源代码管理功能，请导入页面。 有关详细信息，请参阅[从现有 SharePoint 站点导入项目](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)。

 由于在导入这些页面后，很难修改这些页面，因此，在导入这些页面之前，您应该对它们进行设计。

## <a name="create-cascading-style-sheets-ecmascript-and-themes"></a>创建级联样式表、ECMAScript 和主题
 Visual Studio 不提供用于开发 SharePoint 站点的级联样式表（CSS）、ECMAScript （JavaScript、JScript）或主题文件的模板。 可以通过使用 SharePoint SDK 中提供的指南或使用 SharePoint Designer 等工具来创建这些文件。

 可以直接将这些文件添加到解决方案中，也可以导入它们。 在任一情况下，都必须为添加的每个项创建适当的映射文件夹。 有关如何创建映射文件夹的详细信息，请参阅[如何：添加和删除映射文件夹](../sharepoint/how-to-add-and-remove-mapped-folders.md)。

 有关创建级联样式表的详细信息，请参阅[级联样式表 SharePoint Foundation 中的类用法](/previous-versions/office/developer/sharepoint-2010/ms438349(v=office.14))。 有关为 SharePoint 解决方案创建 JavaScript 和 JScript 文件的详细信息，请参阅[为 ECMAScript 设置基本 ASPX 页面](/previous-versions/office/developer/sharepoint-2010/ee535709(v=office.14))。 有关主题的详细信息，请参阅 [构建基块：页面和用户界面](/previous-versions/office/developer/sharepoint-2010/ee539040(v=office.14))。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)|介绍如何添加应用程序页：与 SharePoint 母版页合并的 *.aspx*内容。|
|[如何：创建应用程序页](../sharepoint/how-to-create-an-application-page.md)|演示如何创建在 SharePoint 站点上运行的 ASP.NET 页。|
|[演练：创建 SharePoint 应用程序页](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)|说明如何设计和调试 SharePoint 站点的 ASP.NET 网页。|
