---
title: 为 SharePoint 创建 Web 部件 | Microsoft Docs
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
ms.openlocfilehash: 4824c358f81f2cf757f037611ed70ba9b8935130
ms.sourcegitcommit: 7a46232242783ebe23f2527f91eac8eb84b3ae05
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90740152"
---
# <a name="create-web-parts-for-sharepoint"></a>为 SharePoint 创建 Web 部件
  通过使用 Web 部件，你可以使用浏览器来修改 SharePoint 站点页的内容、外观和行为。 Web 部件是在 Web 部件页中运行的服务器端控件：它们是在 SharePoint 站点上显示的页的构建基块。 请参阅[构建基块：Web 部件](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))。

 可以使用 Visual Studio 中的模板在 SharePoint 站点上创建和调试 Web 部件。

## <a name="create-a-web-part-in-visual-studio"></a>在 Visual Studio 中创建 Web 部件
 通过向任何 SharePoint 项目添加“Web 部件”项来创建 Web 部件。 可以在沙盒解决方案或场解决方案中使用“Web 部件”项。

 如果要使用设计器直观地设计 Web 部件，请创建“可视 Web 部件”项目或将“可视 Web 部件”项添加到任何 SharePoint 项目中 。 仅可在场解决方案中使用“可视 Web 部件”项。

### <a name="web-part-item"></a>Web 部件项
 “Web 部件”项提供可用于为 SharePoint 站点设计 Web 部件的文件。 添加“Web 部件”项时，Visual Studio 会在项目中创建一个文件夹，然后将多个文件添加到该文件夹中。 下表对每个文件进行了描述。

|文件|说明|
|----------|-----------------|
|Elements.xml|包含项目中的功能定义文件用于部署 Web 部件的信息。|
|.webpart 文件|提供 SharePoint 在 Web 部件库中显示 Web 部件所需的信息。|
|代码文件|包含将控件添加到 Web 部件并在 Web 部件内生成自定义内容的方法。|

 有关详细信息，请参阅[如何：创建 SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)。

### <a name="visual-web-part-item"></a>可视 Web 部件项
 可视 Web 部件是使用 Visual Studio 中的可视 Web 开发者设计器创建的 Web 部件。 可视 Web 部件的功能与任何其他 Web 部件相同。 要向 Web 部件添加控件（如按钮和文本框），请将代码添加到 XML 文件。 但是，可以通过将控件从 Visual Studio 工具箱拖放或复制到 Web 部件，将其添加到可视 Web 部件。 然后，设计器会在 XML 文件中生成所需的代码。 请参阅[如何：使用设计器创建 SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)。

## <a name="sharepoint-controls"></a>SharePoint 控件
 Visual Studio 提供了一些用于创建 SharePoint 页的控件（如应用程序页）。 这些控件显示在“工具箱”中的“SharePoint 控件”下 。 这些控件的功能派生自 [Microsoft.SharePoint.WebControls](/previous-versions/office/sharepoint-server/ms413880(v=office.15)) 命名空间，该命名空间包含在 SharePoint 站点和列表页上使用的 ASP.NET 服务器控件。

|控件名称|说明|
|------------------|-----------------|
|[AspMenu](/previous-versions/office/sharepoint-server/ms454108(v=office.15))|插入 ASP 菜单。 有关详细信息，请参阅[菜单控件概述](/previous-versions/ecs0x9w5(v=vs.140))。|
|[CssLink](/previous-versions/office/sharepoint-server/ms439048(v=office.15))|将 LINK 元素插入 .aspx 页，并应用由 CssRegistration 定义的一个或多个外部样式表。|
|[DateTimeControl](/previous-versions/office/sharepoint-server/ms414993(v=office.15))|将日期/时间控件插入 .aspx 页。|
|[FormDigest](/previous-versions/office/sharepoint-server/ms416616(v=office.15))|将安全验证插入 .aspx 页|
|[ListProperty](/previous-versions/office/sharepoint-server/ms455032(v=office.15))|返回指定列表的属性。|
|[ProjectProperty](/previous-versions/office/sharepoint-server/ms478990(v=office.15))|返回当前网站的全局属性。|
|[RssLink](/previous-versions/office/sharepoint-server/ms457574(v=office.15))|将 RSS 源的链接插入 .aspx 页。|
|[ScriptLink](/previous-versions/office/sharepoint-server/ms411959(v=office.15))|提供用于在页上注册资源（如脚本）以便在呈现页时可以请求这些资源的属性和方法。|
|[主题](/previous-versions/office/sharepoint-server/ms460735(v=office.15))|将主题应用到 .aspx 页。|

## <a name="debug-a-web-part"></a>调试 Web 部件
 可以像调试其他 Visual Studio 项目一样，调试包含 Web 部件的 SharePoint 项目。 当你启动 Visual Studio 调试器时，Visual Studio 将打开 SharePoint 站点。

 若要开始调试代码，请将 Web 部件添加到 SharePoint 中的 Web 部件页。

 有关如何调试 SharePoint 项目的详细信息，请参阅 [SharePoint 解决方案疑难解答](../sharepoint/troubleshooting-sharepoint-solutions.md)。

## <a name="visual-web-part-limitations"></a>可视 Web 部件限制
 从 Visual Studio 开始，可以将可视 Web 部件添加到沙盒 SharePoint 解决方案和场解决方案。 但是，可视 Web 部件具有以下限制：

- 可视 Web 部件不支持可替换参数。 有关详细信息，请参阅[可替换参数](../sharepoint/replaceable-parameters.md)。

- 不能将用户控件或可视 Web 部件拖放或复制到可视 Web 部件。 此操作会导致生成错误。

- 可视 Web 部件不直接支持 SharePoint 服务器令牌，如 $SPUrl。 有关详细信息，请参阅 [SharePoint 解决方案疑难解答](../sharepoint/troubleshooting-sharepoint-solutions.md)主题中的“沙盒可视 Web 部件中的令牌限制”。

- 沙盒解决方案中的可视 Web 部件偶尔会出现以下错误：“已拒绝沙盒代码执行请求，因为沙盒代码主机服务太忙，无法处理该请求”。 有关此错误的详细信息，请参阅 [SharePoint 开发者团队博客](/archive/blogs/sharepointdev/error-the-sandboxed-code-execution-request-was-refused-because-the-sandboxed-code-host-service-was-too-busy-to-handle-the-request-ricky-kirkham#10149157)中的这篇博文。

- Visual Studio 不支持服务器端 JavaScript 调试，但支持客户端 JavaScript 调试。

   虽然可以将内联 JavaScript 添加到服务器端标记文件，但不支持对添加到标记的断点进行调试。 若要调试 JavaScript，请在标记文件中引用外部 JavaScript 文件，然后在 JavaScript 文件中设置断点。

- 必须在生成的代码文件而不是标记文件中进行内联 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 代码的调试。

- 可视 Web 部件不支持使用 `<@ Assembly Src=` 指令。

- SharePoint Web 控件和某些 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 控件在 SharePoint 沙盒环境中不受支持。 如果在沙盒解决方案的可视 Web 部件上使用不受支持的控件，则会出现以下错误：“命名空间‘Microsoft.SharePoint.WebControls’中不存在类型或命名空间名称‘Theme’”。

  有关沙盒解决方案的详细信息，请参阅[沙盒解决方案与场解决方案之间的差异](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)。

## <a name="create-older-style-sharepoint-based-web-parts"></a>创建基于 SharePoint 的旧式 Web 部件
 可以使用 Visual Studio 中的模板为 SharePoint 创建自定义 [!INCLUDE[vstecasplong](../sharepoint/includes/vstecasplong-md.md)] Web 部件。 [!INCLUDE[vstecasplong](../sharepoint/includes/vstecasplong-md.md)] Web 部件在 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] Web 部件基础结构之上构建，是新项目的建议类型。

 在极少数情况下，可能必须使用基于 SharePoint 的旧式 Web 部件来创建 Web 部件。 可以使用 Visual Studio 来创建这些类型的 Web 部件，但 Visual Studio 不提供任何专门设计的模块来帮助你创建这些部件。

 有关何时需要创建基于 SharePoint 的旧式 Web 部件的详细信息，请参阅 [Windows SharePoint Services 中的 Web 部件基础结构](/previous-versions/office/developer/sharepoint-2010/ms415560(v=office.14))。 有关如何使用基于 SharePoint 的旧式 Web 部件创建 Web 部件的详细信息，请参阅[演练 - 创建基本 SharePoint Web 部件](/previous-versions/office/ms452873(v=office.14))。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[如何：创建 SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)|演示如何为 SharePoint 页创建 Web 部件。|
|[如何：使用设计器创建 SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)|演示如何使用视觉设计图面为 SharePoint 创建 Web 部件。|
|[如何：为 SharePoint 应用程序页或 Web 部件创建用户控件](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)|演示如何创建可由 SharePoint 中运行的应用程序页和 Web 部件使用的自定义可重用控件。|
|[演练：为 SharePoint 创建 Web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)|介绍如何为 SharePoint 设计 Web 部件。|
|[演练：使用设计器为 SharePoint 创建 Web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)|介绍如何通过将控件拖动到视觉设计图面来为 SharePoint 设计 Web 部件。|
|[演练：创建显示用于 SharePoint 的 OData 的 Silverlight Web 部件](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)|介绍如何设计承载 Silverlight 应用程序并显示 SharePoint 列表中数据的 SharePoint Web 部件。|