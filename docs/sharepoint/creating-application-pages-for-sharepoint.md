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
ms.openlocfilehash: 8ac9340ea853a1852d039f05a3ecbb100845ab84
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443538"
---
# <a name="create-application-pages-for-sharepoint"></a>为 SharePoint 创建应用程序页
  *应用程序页*是专为在 SharePoint 网站中使用的 ASP.NET 网页。 应用程序页面是 ASP.NET 页的专用化的类型。 应用程序页和一个标准的 ASP.NET 页面的主要区别是应用程序页包含与 SharePoint 母版页合并的内容。 母版页使应用程序页作为站点上的其他页面共享相同的外观和行为。

 Visual Studio，可使用设计器中设计应用程序页。 在设计器显示在母版页中定义的每个内容占位符的内容区域。 您可以设计应用程序页上，通过将控件拖到这些内容区域。

## <a name="application-pages"></a>应用程序页
 而站点页面是特定于一个站点服务器上的所有站点上共享应用程序页。 有关详细信息[SharePoint 页面类型](http://go.microsoft.com/fwlink/?LinkID=211584)。

 默认情况下，当你创建一个 SharePoint 站点时，显示的页面的大部分都是站点页面。 网站页面可以添加到 SharePoint 页库。 通过使用诸如 SharePoint Designer 之类的工具，用户可以自定义的网站页面。 网站页面也可以承载功能，例如动态 Web 部件和 Web 部件区域。

 应用程序页不能执行这些操作。 但是应用程序页是页的最适合后，可以创建如果你想要包含自定义代码的页。 虽然可以将自定义代码添加到站点页面，在代码停止运行时在用户通过使用诸如 SharePoint Designer 之类的工具自定义页。

> [!NOTE]
> Visual Studio 不提供模板，帮助你创建的 SharePoint 站点的站点页面。 有关详细信息，请参阅[SharePoint 页面类型](http://go.microsoft.com/fwlink/?LinkID=211584)。

## <a name="create-an-application-page"></a>创建应用程序页
 若要创建的应用程序页，添加**应用程序页**向 SharePoint 项目项。 创建应用程序页，在 Visual Studio 将添加到你的项目的以下文件夹：

|文件夹|描述|
|------------|-----------------|
|布局|映射到 SharePoint 文件系统的 _layouts 虚拟目录。|
|布局子文件夹|包含构成应用程序页上的文件。 默认情况下，此文件夹包含与项目相同的名称。 你可以随时重命名此文件夹。 运行项目时，Visual Studio 会将此文件夹部署到 SharePoint 文件系统的 _layouts 虚拟目录。|

 Visual Studio 将以下文件添加到你的项目：

|文件|描述|
|----------|-----------------|
|ASP.NET 页文件 (*.aspx*)|包含定义的页面的 XML 标记。|
|应用程序页代码文件|包含代码隐藏的应用程序页。 添加代码来处理此文件的事件。|
|应用程序页设计器代码文件|包含设计器生成的代码。 不要直接编辑此文件。|

## <a name="design-and-debug-an-application-page"></a>设计和调试应用程序页
 通过使用 Visual Studio 中的设计器视图来设计应用程序页的内容。 在项目中打开应用程序页上时显示此设计器 (通过双击它或打开其快捷菜单，然后选择**打开**)，然后选择**设计**底部的按钮在编辑器中。

> [!NOTE]
> 您可以设计页仅在**源**在设计器视图。 **设计**为应用程序页禁用设计器的视图。

 您可以调试应用程序页，就像就像调试其他 Visual Studio 中的 SharePoint 项目项。 启动 Visual Studio 调试器时，Visual Studio 会打开 SharePoint 站点。

 若要查看应用程序页上，您必须手动导航到应用程序页的位置 (例如： http://<em>Server_Name</em>/_layouts/*Project_Name*/ApplicationPage1.aspx)。

 有关如何调试 SharePoint 项目的详细信息，请参阅[进行故障排除 SharePoint 解决方案](../sharepoint/troubleshooting-sharepoint-solutions.md)。

## <a name="choose-a-master-page"></a>选择母版页
 默认情况下**应用程序页**项引用要用来调试你的项目的站点的母版页。 页名为 v4.master，可以发现它列在**母版页样式库**的 SharePoint 站点。

 您可以显式更改设置的应用程序页使用的母版页`MasterPageFile`属性的应用程序的`Page`元素。 (例如： `MasterPageFile="~/_layouts/applicationv4.master"`)。 事实上，如果在 SharePoint 服务器上未启用动态母版页，则必须设置此属性。 有关在 SharePoint 中母版页的详细信息，请参阅[母版页](http://go.microsoft.com/fwlink/?LinkID=169281)。

## <a name="see-also"></a>请参阅
- [SharePoint Foundation 开发详解](http://go.microsoft.com/fwlink/?LinkID=182103)
- [ASP.NET 概述](/aspnet/overview)
- [ASP.NET 网页](/aspnet/web-pages/index)
