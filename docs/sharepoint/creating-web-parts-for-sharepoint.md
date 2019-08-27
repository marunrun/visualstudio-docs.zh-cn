---
title: 为 SharePoint 创建 Web 部件 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 1105e6c68e1ec9083fd790ad8a38b09870345af2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62580938"
---
# <a name="create-web-parts-for-sharepoint"></a>为 SharePoint 创建 web 部件
  通过使用 web 部件，可以使用浏览器中修改内容、 外观和行为的 SharePoint 站点页面。 Web 部件是在 web 部件页中运行的服务器端控件： 它们是在 SharePoint 网站显示的页的构建基块。 请参阅[构建基块：Web 部件](http://go.microsoft.com/fwlink/?LinkID=182097)。

 可以创建和使用模板从 Visual Studio 调试在 SharePoint 站点上的 web 部件。

## <a name="create-a-web-part-in-visual-studio"></a>在 Visual Studio 中创建 web 部件
 通过添加创建的 web 部件**Web 部件**向任何 SharePoint 项目项。 可以使用**Web 部件**沙盒解决方案或场解决方案中的项。

 如果你想要使用设计器直观地设计 web 部件中，创建**可视 Web 部件**项目或添加**可视 Web 部件**向任何 SharePoint 项目项。 可以使用**可视 Web 部件**场解决方案中的项。

### <a name="web-part-item"></a>Web 部件项
 一个**Web 部件**项提供了可用于设计 web 部件的 SharePoint 站点的文件。 当您将添加**Web 部件**项，Visual Studio 项目中创建一个文件夹，然后将多个文件添加到的文件夹。 下表介绍每个文件。

|文件|描述|
|----------|-----------------|
|*Elements.xml*|包含在项目中的功能定义文件用于部署 web 部件的信息。|
|.webpart 文件|提供 SharePoint web 部件库中显示 web 部件所需的信息。|
|代码文件|包含的方法，将控件添加到 web 部件和生成 web 部件中的自定义内容。|

 有关详细信息，请参阅[如何：创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)。

### <a name="visual-web-part-item"></a>可视 web 部件项
 可视 web 部件是您在 Visual Studio 中使用 Visual Web Developer 设计器创建的 web 部件。 可视 web 部件功能与任何其他 web 部件相同。 若要添加到 web 部件控件，如按钮和文本框中，您将代码添加到 XML 文件。 但是，您将控件添加到可视 web 部件拖动或复制到 web 部件上从 Visual Studio**工具箱**。 在设计器在 XML 文件中然后生成所需的代码。 请参阅[如何：使用设计器创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)。

## <a name="sharepoint-controls"></a>SharePoint 控件
 Visual Studio 提供了一些控件，用于创建 SharePoint 页，如应用程序页。 这些控件显示在**工具箱**下**SharePoint 控件**。 这些控件的功能派生[Microsoft.SharePoint.WebControls](http://go.microsoft.com/fwlink/?LinkId=235315)命名空间，其中包含 SharePoint 站点和列表页面所使用的 ASP.NET 服务器控件。

|控件名称|描述|
|------------------|-----------------|
|[AspMenu](http://go.microsoft.com/fwlink/?LinkId=235307)|插入 ASP 菜单。 有关详细信息，请参阅[菜单控件概述](http://go.microsoft.com/fwlink/?LinkId=235316)。|
|[CssLink](http://go.microsoft.com/fwlink/?LinkId=235308)|将插入**链接**元素插入 *.aspx*页上，并应用一个或多个外部样式表由定义**CssRegistration**。|
|[DateTimeControl](http://go.microsoft.com/fwlink/?LinkId=235306)|将插入将 DateTime 控件插入 *.aspx*页。|
|[FormDigest](http://go.microsoft.com/fwlink/?LinkId=235309)|将插入到安全验证 *.aspx*页|
|[ListProperty](http://go.microsoft.com/fwlink/?LinkId=235310)|返回指定列表的属性。|
|[ProjectProperty](http://go.microsoft.com/fwlink/?LinkId=235311)|返回当前网站的全局属性。|
|[RssLink](http://go.microsoft.com/fwlink/?LinkId=235312)|将插入到 RSS 源的链接 *.aspx*页。|
|[ScriptLink](http://go.microsoft.com/fwlink/?LinkId=235313)|提供了用于注册资源，例如脚本、 在页面上，以便他们可以请求页面呈现时属性和方法。|
|[主题](http://go.microsoft.com/fwlink/?LinkId=235314)|应用到主题 *.aspx*页。|

## <a name="debug-a-web-part"></a>调试 web 部件
 您可以调试包含 web 部件，就像就像调试其他 Visual Studio 项目的 SharePoint 项目。 启动 Visual Studio 调试器时，Visual Studio 会打开 SharePoint 站点。

 若要开始调试代码，将添加到 SharePoint 中的 web 部件页的 web 部件。

 有关如何调试 SharePoint 项目的详细信息，请参阅[进行故障排除 SharePoint 解决方案](../sharepoint/troubleshooting-sharepoint-solutions.md)。

## <a name="visual-web-part-limitations"></a>可视 web 部件限制
 从 Visual Studio 中，可以将可视 web 部件添加到沙盒 SharePoint 解决方案和场解决方案。 但是，可视 web 部件具有以下限制：

- Visual web 部件不支持可替换参数。 有关详细信息，请参阅[可替换参数](../sharepoint/replaceable-parameters.md)。

- 不能拖动和删除或复制到可视 web 部件上的用户控件或可视 web 部件。 此操作会导致生成错误。

- 可视 web 部件不直接支持 SharePoint 服务器标记，如 $SPUrl。 详细信息，请参阅"令牌限制在沙盒可视 Web 部件"主题中[进行故障排除 SharePoint 解决方案](../sharepoint/troubleshooting-sharepoint-solutions.md)。

- 沙盒解决方案中的可视 web 部件偶尔会发生错误，"沙盒代码执行请求已被拒绝，因为沙盒代码托管服务太忙而无法处理该请求。" 有关此错误的详细信息，请参阅中的该文章[SharePoint 开发人员团队博客](http://go.microsoft.com/fwlink/?LinkId=225932)。

- 服务器端 JavaScript 调试不支持在 Visual Studio 中，但客户端 JavaScript 调试支持。

   尽管可以将内联 JavaScript 添加到服务器端标记文件，但不支持断点添加到标记的调试。 若要调试 JavaScript，引用外部 JavaScript 文件中的标记文件，然后在 JavaScript 文件中设置断点。

- 调试内联[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]代码必须在标记文件中而不是生成的代码文件中完成。

- 可视 web 部件不支持使用`<@ Assembly Src=`指令。

- SharePoint web 控件以及一些[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]控件不受支持 SharePoint 沙盒环境中。 如果不受支持的控件用于在可视 web 部件在沙盒解决方案中，该错误，会显示"的类型或命名空间名称 '主题' 命名空间 'Microsoft.SharePoint.WebControls' 中不存在"。

  有关沙盒解决方案的详细信息，请参阅[区别沙盒解决方案与场解决方案](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)。

## <a name="create-older-style-sharepoint-based-web-parts"></a>创建基于 SharePoint 的 web 部件的较旧样式
 可以使用 Visual Studio 中的模板来创建自定义[!INCLUDE[vstecasplong](../sharepoint/includes/vstecasplong-md.md)]的 SharePoint web 部件。 [!INCLUDE[vstecasplong](../sharepoint/includes/vstecasplong-md.md)] web 部件构建的[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]web 部件基础结构并为新项目的推荐类型。

 在极少数情况下，可能需要使用较旧样式的基于 SharePoint 的 web 部件创建 web 部件。 可以使用 Visual Studio 来创建这些类型的 web 部件，但 Visual Studio 不提供专门用来帮助你创建它们的任何模板。

 当你可能想要创建较旧样式的基于 SharePoint 的 web 部件的详细信息，请参阅[Windows SharePoint Services 中的 Web 部件基础结构](http://go.microsoft.com/fwlink/?LinkId=169290)。 有关如何使用较旧样式的基于 SharePoint 的 web 部件创建 web 部件的详细信息，请参阅[创建一个基本的 SharePoint Web 部件的演练](http://go.microsoft.com/fwlink/?LinkId=169288)。

## <a name="related-topics"></a>相关主题

|标题|说明|
|-----------|-----------------|
|[如何：创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)|演示如何创建 web 部件的 SharePoint 页。|
|[如何：使用设计器创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)|演示如何通过使用一个可视化设计图面为 SharePoint 创建 web 部件。|
|[如何：创建 SharePoint 应用程序页或 web 部件的用户控件](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)|演示如何创建可由应用程序页和在 SharePoint 中运行的 web 部件使用的自定义可重用控件。|
|[演练：为 SharePoint 创建 web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)|介绍如何为 SharePoint 设计 web 部件。|
|[演练：使用设计器为 SharePoint 创建 web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)|介绍如何通过将控件拖动到可视化设计图面为 SharePoint 设计 web 部件。|
|[演练：创建显示 SharePoint OData 的 Silverlight web 部件](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)|介绍如何为承载 Silverlight 应用程序并显示来自 SharePoint 列表数据的 SharePoint 设计 web 部件。|
