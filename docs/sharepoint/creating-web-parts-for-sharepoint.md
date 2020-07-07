---
title: 为 SharePoint 创建 Web 部件 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
f1_keywords:
- Microsoft.SharePoint.WebControls.DateTimeControl
- Microsoft.SharePoint.WebControls.CssLink
- Microsoft.SharePoint.WebControls.RssLink
- Microsoft.SharePoint.WebControls.Theme
- Microsoft.SharePoint.WebControls.AspMenu
- Microsoft.SharePoint.WebControls.ListProperty
- Microsoft.SharePoint.WebControls.ProjectProperty
- Microsoft.SharePoint.WebControls.FormsDigest
- Microsoft.SharePoint.WebControls.ScriptLink
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, Web Parts
- Web Parts [SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3825ef7d2c1c90f63a90f5028063c74332543841
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015054"
---
# <a name="create-web-parts-for-sharepoint"></a>为 SharePoint 创建 web 部件
  通过使用 web 部件，你可以通过使用浏览器来修改 SharePoint 站点的页面的内容、外观和行为。 Web 部件是在 web 部件页中运行的服务器端控件：它们是在 SharePoint 站点上显示的页的构建基块。 请参阅[构建基块： Web 部件](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))。

 您可以使用 Visual Studio 中的模板在 SharePoint 站点上创建和调试 web 部件。

## <a name="create-a-web-part-in-visual-studio"></a>在 Visual Studio 中创建 web 部件
 通过向任何 SharePoint 项目添加 " **Web 部件**" 项来创建 web 部件。 您可以使用沙盒解决方案或场解决方案中的 " **Web 部件**" 项。

 如果要使用设计器以可视方式设计 web 部件，请创建一个**可视 Web 部件**项目或将 "**可视 web 部件**" 项添加到任何 SharePoint 项目。 您只能使用场解决方案中的**可视 Web 部件**项。

### <a name="web-part-item"></a>Web 部件项
 **Web 部件**项提供的文件可用于设计 SharePoint 站点的 Web 部件。 添加**Web 部件**项时，Visual Studio 会在项目中创建一个文件夹，然后将多个文件添加到该文件夹中。 下表对每个文件进行了说明。

|文件|说明|
|----------|-----------------|
|*Elements.xml*|包含项目中的功能定义文件用于部署 web 部件的信息。|
|webpart 文件|提供 SharePoint 在 web 部件库中显示 web 部件所需的信息。|
|代码文件|包含一些方法，这些方法可向 web 部件添加控件，并在 web 部件中生成自定义内容。|

 有关详细信息，请参阅[如何：创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)。

### <a name="visual-web-part-item"></a>可视 web 部件项
 可视 web 部件是使用 visual Studio 中的 Visual Web Developer 设计器创建的 web 部件。 可视 web 部件的功能与任何其他 web 部件相同。 若要向 web 部件添加控件（如按钮和文本框），请将代码添加到 XML 文件。 但是，您可以通过将控件从 Visual Studio **"工具箱**" 拖动或复制到 web 部件来向可视 web 部件添加控件。 然后，设计器会在 XML 文件中生成所需的代码。 请参阅[如何：使用设计器创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)。

## <a name="sharepoint-controls"></a>SharePoint 控件
 Visual Studio 提供了一些用于创建 SharePoint 页（如应用程序页）的控件。 这些控件出现在**SharePoint 控件**下的**工具箱**中。 这些控件的功能派生自[WebControls](/previous-versions/office/sharepoint-server/ms413880(v=office.15))命名空间，该命名空间包含在 SharePoint 站点和列表页上使用的 ASP.NET 服务器控件。

|控件名称|说明|
|------------------|-----------------|
|[AspMenu](/previous-versions/office/sharepoint-server/ms454108(v=office.15))|插入 ASP 菜单。 有关详细信息，请参阅[菜单控件概述](/previous-versions/ecs0x9w5(v=vs.140))。|
|[CssLink](/previous-versions/office/sharepoint-server/ms439048(v=office.15))|将**LINK**元素插入 *.aspx*页面，并应用一个或多个由**CssRegistration**定义的外部样式表。|
|[DateTimeControl](/previous-versions/office/sharepoint-server/ms414993(v=office.15))|将日期时间控件插入 *.aspx*页中。|
|[FormDigest](/previous-versions/office/sharepoint-server/ms416616(v=office.15))|在 *.aspx*页中插入安全验证|
|[ListProperty](/previous-versions/office/sharepoint-server/ms455032(v=office.15))|返回指定列表的属性。|
|[ProjectProperty](/previous-versions/office/sharepoint-server/ms478990(v=office.15))|返回当前网站的全局属性。|
|[.Rsslink](/previous-versions/office/sharepoint-server/ms457574(v=office.15))|将 RSS 源的链接插入 *.aspx*页中。|
|[ScriptLink](/previous-versions/office/sharepoint-server/ms411959(v=office.15))|提供用于在页面上注册资源（如脚本）的属性和方法，以便在呈现页面时可以请求这些资源。|
|[主题](/previous-versions/office/sharepoint-server/ms460735(v=office.15))|将主题应用于 *.aspx*页。|

## <a name="debug-a-web-part"></a>调试 web 部件
 可以像调试其他 Visual Studio 项目一样，调试包含 web 部件的 SharePoint 项目。 当你启动 Visual Studio 调试器时，Visual Studio 将打开 SharePoint 站点。

 若要开始调试代码，请将 web 部件添加到 SharePoint 中的 web 部件页。

 有关如何调试 SharePoint 项目的详细信息，请参阅[排查 sharepoint 解决方案问题](../sharepoint/troubleshooting-sharepoint-solutions.md)。

## <a name="visual-web-part-limitations"></a>可视 web 部件限制
 从 Visual Studio 开始，可以将可视 web 部件添加到沙盒 SharePoint 解决方案和场解决方案。 但是，可视 web 部件具有以下限制：

- 可视 web 部件不支持可替换参数。 有关详细信息，请参阅可[替换参数](../sharepoint/replaceable-parameters.md)。

- 不能将用户控件或可视 web 部件拖放或复制到可视 web 部件。 此操作会导致生成错误。

- 可视 web 部件不直接支持 SharePoint 服务器标记，如 $SPUrl。 有关详细信息，请参阅[SharePoint 解决方案疑难解答](../sharepoint/troubleshooting-sharepoint-solutions.md)主题中的 "沙盒 Visual Web 部件中的令牌限制"。

- 沙盒解决方案中的可视 web 部件偶尔出现错误 "已拒绝沙盒代码执行请求，因为沙盒代码主机服务太忙，无法处理该请求"。 有关此错误的详细信息，请参阅[SharePoint 开发人员团队博客](https://blogs.msdn.microsoft.com/sharepointdev/2011/02/08/error-the-sandboxed-code-execution-request-was-refused-because-the-sandboxed-code-host-service-was-too-busy-to-handle-the-request-ricky-kirkham/#10149157)中的此文章。

- Visual Studio 不支持服务器端 JavaScript 调试，但支持客户端 JavaScript 调试。

   虽然可以将内联 JavaScript 添加到服务器端标记文件，但添加到标记的断点不支持调试。 若要调试 JavaScript，请在标记文件中引用外部 JavaScript 文件，然后在 JavaScript 文件中设置断点。

- [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]必须在生成的代码文件而不是标记文件中对内联代码进行调试。

- 可视 web 部件不支持使用 `<@ Assembly Src=` 指令。

- Sharepoint web 控件和某些 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 控件在 sharepoint 沙盒环境中不受支持。 如果在沙盒解决方案中的可视 web 部件上使用不受支持的控件，则会出现 "WebControls" 命名空间中不存在 "类型或命名空间名称" 主题。

  有关沙盒解决方案的详细信息，请参阅[沙盒解决方案与场解决方案之间的差异](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)。

## <a name="create-older-style-sharepoint-based-web-parts"></a>创建旧样式的基于 SharePoint 的 web 部件
 您可以使用 Visual Studio 中的模板为 SharePoint 创建自定义 [!INCLUDE[vstecasplong](../sharepoint/includes/vstecasplong-md.md)] web 部件。 [!INCLUDE[vstecasplong](../sharepoint/includes/vstecasplong-md.md)]web 部件构建在 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] web 部件基础结构之上，是新项目的建议类型。

 在极少数情况下，可能必须使用基于 SharePoint 的旧版 web 部件来创建 web 部件。 您可以使用 Visual Studio 来创建这些类型的 web 部件，但 Visual Studio 不提供专门为帮助您创建的模板。

 若要详细了解何时想要创建较旧样式的基于 SharePoint 的 web 部件，请参阅[Windows Sharepoint Services 中的 Web 部件基础结构](/previous-versions/office/developer/sharepoint-2010/ms415560(v=office.14))。 有关如何使用较旧样式的基于 SharePoint 的 web 部件创建 web 部件的详细信息，请参阅[创建基本 Sharepoint Web 部件的演练](/previous-versions/office/ms452873(v=office.14))。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[如何：创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)|说明如何为 SharePoint 页面创建 web 部件。|
|[如何：使用设计器创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)|演示如何使用可视化设计图面为 SharePoint 创建 web 部件。|
|[如何：为 SharePoint 应用程序页或 web 部件创建用户控件](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)|演示如何创建可由在 SharePoint 中运行的应用程序页和 web 部件使用的自定义的可重用控件。|
|[演练：为 SharePoint 创建 web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)|描述如何为 SharePoint 设计 web 部件。|
|[演练：使用设计器为 SharePoint 创建 web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)|介绍如何通过将控件拖到可视化设计图面来为 SharePoint 设计 web 部件。|
|[演练：创建显示 OData for SharePoint 的 Silverlight web 部件](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)|介绍如何设计承载 Silverlight 应用程序的 SharePoint web 部件并显示 SharePoint 列表中的数据。|
