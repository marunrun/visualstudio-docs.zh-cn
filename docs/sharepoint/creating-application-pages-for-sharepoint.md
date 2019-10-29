---
title: 为 SharePoint 创建应用程序页 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, Web pages
- SharePoint development in Visual Studio, content pages
- SharePoint development in Visual Studio, application pages
- application pages [SharePoint development in Visual Studio], developing
- application pages [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 47f403f4eec6ec66563ae88bec226e073f625716
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72981103"
---
# <a name="create-application-pages-for-sharepoint"></a>为 SharePoint 创建应用程序页
  *应用程序页*是设计为在 SharePoint 网站中使用的 ASP.NET 网页。 应用程序页是特定类型的 ASP.NET 页。 应用程序页和标准 ASP.NET 页之间的主要区别在于，应用程序页包含与 SharePoint 母版页合并的内容。 母版页使应用程序页面与站点上的其他页面共享相同的外观和行为。

 利用 Visual Studio，你可以通过使用设计器来设计应用程序页。 设计器显示在母版页中定义的每个内容占位符的内容区域。 您可以通过将控件拖到这些内容区域来设计应用程序页。

## <a name="application-pages"></a>应用程序页
 应用程序页在服务器上的所有站点之间共享，而站点页面则特定于一个站点。 有关详细信息，请查看[SharePoint 页面类型](/previous-versions/office/developer/sharepoint-2010/aa979592(v=office.14))。

 默认情况下，创建 SharePoint 站点时显示的大多数页面都是网站页面。 网站页面可以添加到 SharePoint 页面库。 用户可以使用 SharePoint Designer 等工具来自定义网站页面。 网站页面还可以托管功能，如动态 Web 部件和 Web 部件区域。

 应用程序页不能执行这些操作。 但是，如果您希望页面包含自定义代码，则可以创建一个应用程序页。 虽然您可以将自定义代码添加到站点页，但当用户使用 SharePoint Designer 等工具自定义该页时，代码将停止运行。

> [!NOTE]
> Visual Studio 不提供帮助您为 SharePoint 站点创建网站页面的模板。 有关详细信息，请参阅[SharePoint 页面类型](/previous-versions/office/developer/sharepoint-2010/aa979592(v=office.14))。

## <a name="create-an-application-page"></a>"创建应用程序" 页
 若要创建应用程序页，请向 SharePoint 项目添加 "**应用程序页**" 项。 当你创建应用程序页时，Visual Studio 会将以下文件夹添加到你的项目：

|文件夹|描述|
|------------|-----------------|
|布局|映射到 SharePoint 文件系统的 _layouts 虚拟目录。|
|布局子文件夹|包含构成应用程序页面的文件。 默认情况下，此文件夹具有与项目相同的名称。 你可以随时重命名此文件夹。 运行该项目时，Visual Studio 会将此文件夹部署到 SharePoint 文件系统的 _layouts 虚拟目录。|

 Visual Studio 会将以下文件添加到项目中：

|文件|描述|
|----------|-----------------|
|ASP.NET 页文件（ *.aspx*）|包含用于定义该页的 XML 标记。|
|应用程序页代码文件|包含应用程序页后的代码。 将处理事件的代码添加到此文件。|
|应用程序页设计器代码文件|包含由设计器生成的代码。 不要直接编辑此文件。|

## <a name="design-and-debug-an-application-page"></a>设计和调试应用程序页
 使用 Visual Studio 中的设计器视图设计应用程序页的内容。 当您在项目中打开应用程序页（通过双击或打开其快捷菜单，然后选择 "**打开**"），然后选择编辑器底部的 "**设计**" 按钮时，将显示此设计器。

> [!NOTE]
> 您只能在设计器的 "**源**" 视图中设计此页。 对于应用程序页，禁用设计器的**设计**视图。

 可以像调试 Visual Studio 中的其他 SharePoint 项目项一样调试应用程序页。 当你启动 Visual Studio 调试器时，Visual Studio 将打开 SharePoint 站点。

 若要查看应用程序页，必须手动导航到应用程序页的位置（例如： http://<em>Server_Name</em>/_Layouts/*Project_Name*/ApplicationPage1.aspx）。

 有关如何调试 SharePoint 项目的详细信息，请参阅[排查 sharepoint 解决方案问题](../sharepoint/troubleshooting-sharepoint-solutions.md)。

## <a name="choose-a-master-page"></a>选择母版页
 默认情况下，**应用程序页**项引用用于调试项目的站点的母版页。 该页命名为 "v4"，您可以在 SharePoint 站点的**母版页库**中找到它。

 可以通过设置应用程序 `Page` 元素的 `MasterPageFile` 特性来显式更改应用程序页所使用的母版页。 （例如： `MasterPageFile="~/_layouts/applicationv4.master"`）。 事实上，如果在 SharePoint 服务器上未启用动态母版页，则必须设置此属性。 有关 SharePoint 中的母版页的详细信息，请参阅[母版页](/previous-versions/office/developer/sharepoint-2010/ms443795(v=office.14))。

## <a name="see-also"></a>请参阅
- [SharePoint Foundation 开发深入了解](/previous-versions/office/developer/sharepoint-2010/ee539092(v=office.14))
- [ASP.NET 概述](/aspnet/overview)
- [ASP.NET 网页](/aspnet/web-pages/index)
