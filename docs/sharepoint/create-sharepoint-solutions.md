---
title: 创建 SharePoint 解决方案 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2b3138e148ea44371c7bd9b5fb82c583cd00e832
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436415"
---
# <a name="create-sharepoint-solutions"></a>创建 SharePoint 解决方案
  你可以将在 Visual Studio 中创建 SharePoint 应用程序作为在 SharePoint 设计器中创建它们的替代方法。 Visual Studio 可通过提供诸如高级调试工具、IntelliSense、语句完成和项目模板等功能加快对 SharePoint 的开发。 Visual Studio 还会利用基于 .NET Framework 的高级工具和语言。 你可以通过使用 Visual Basic 或 Visual C# 来开发 SharePoint 项目，也可以通过使用 JavaScript 来开发 SharePoint 应用程序。

 有关 SharePoint 2013 和 SharePoint 外接程序的信息，请参阅 [SharePoint 2013](https://products.office.com/previous-versions/microsoft-sharepoint-2013) 和 [构建 SharePoint 应用程序](/sharepoint/dev/sp-add-ins/sharepoint-add-ins)。

> [!NOTE]
> 了解如何使用全新 [SharePoint 外接程序模型](/sharepoint/dev/sp-add-ins/sharepoint-add-ins) 来扩展你的用户的 SharePoint 体验。 与 SharePoint 解决方案相比，这些外接程序的需求量很小，几乎可以使用任何 Web 编程技术（例如 HTML5、JavaScript、CSS3 和 XML）生成。

|||
|-|-|
|![文档](../sharepoint/media/vs-icon-documentation.gif "文档")|**文档**<br /><br /> -   [开始&#40;Visual Studio 中的 SharePoint 开发&#41;](../sharepoint/getting-started-sharepoint-development-in-visual-studio.md)<br />-   [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)<br />-   [本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)<br />-   [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)<br />-   [包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)<br />-   [扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)|
|![文档](../sharepoint/media/vs-icon-documentation.gif "文档")|**特色的任务**<br /><br /> -   [演练：创建 SharePoint 网站栏、 内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)<br />-   [如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)<br />-   [如何：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)<br />-   [如何：创建 SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)<br />-   [如何：创建 SharePoint 应用程序页或 web 部件的用户控件](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)|
|![演练](../sharepoint/media/vs-icon-walkthroughs.gif "演练")|**演练**<br /><br /> -   [SharePoint 开发演练](../sharepoint/sharepoint-development-walkthroughs.md)|
|![代码示例](../sharepoint/media/vs-icon-codesamples.gif "的代码示例")|**代码示例**<br /><br /> -   [SharePoint 开发示例](../sharepoint/sharepoint-development-samples.md)<br />-   [SharePoint 开发人员工具下载](/sharepoint/dev/)|
|![定型](../sharepoint/media/vs-icon-training.gif "培训")|**培训**<br /><br /> -   [了解 SharePoint 开发](/sharepoint/dev/)|
|![论坛](../sharepoint/media/vs-icon-forums.gif "论坛")|**论坛**<br /><br /> -   [使用 Visual Studio 进行 SharePoint 开发](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vssharepointdevelopment)<br />-   [SharePoint 2010](https://social.msdn.microsoft.com/Forums/sharepoint/home?category=sharepoint2010,sharepoint)|
|![定型](../sharepoint/media/vs-icon-training.gif "培训")|**博客**<br /><br /> -   [Visual Studio SharePoint 开发博客](https://blogs.msdn.microsoft.com/vssharepointtoolsblog/)|
|![我如何？视频](../sharepoint/media/vs-icon-howdoivideos.gif "如何操作？视频")|**我如何？视频**<br /><br /> -   [如何实现:在 Visual Studio 2010 中创建用于 SharePoint 2010 可视 Web 部件？](https://visualstudio.microsoft.com/)<br />-   [如何实现:在 Visual Studio 2010 中创建用于 SharePoint 2010 的内容类型？](/previous-versions/visualstudio/visual-studio-2010/dd831853\(v\=vs.100\))<br />-   [如何实现:在 Visual Studio 2010 中创建用于 SharePoint 2010 站点定义？](/previous-versions/visualstudio/visual-studio-2010/dd831853\(v\=vs.100\))<br />-   [如何实现:创建使用 Visual Studio 2010 的 SharePoint 2010 的业务数据连接模型？](/previous-versions/visualstudio/visual-studio-2010/dd831853\(v\=vs.100\))|
|![第 9 频道视频](../sharepoint/media/vs-icon-channel9videos.gif "第 9 频道视频")|**第 9 频道视频**<br /><br /> -   [Visual Studio 2010 中的 SharePoint 开发概述](https://channel9.msdn.com/blogs/funkyonex/overview-of-sharepoint-development-in-visual-studio-2010)<br />-   [使用 Visual Studio 2010 构建 SharePoint 2010 Web 部件的最佳做法](https://channel9.msdn.com/blogs/funkyonex/best-practices-on-building-sharepoint-2010-web-parts-with-visual-studio-2010)<br />-   [Visual Studio 2010 中的 SharePoint 功能和包设计器](https://channel9.msdn.com/blogs/funkyonex/sharepoint-feature-and-package-designers-in-visual-studio-2010)|
|![开发人员中心](../sharepoint/media/vs-icon-msdndevcenter.gif "开发人员中心")|**开发人员中心**<br /><br /> -   [Visual Studio 开发中心](https://visualstudio.microsoft.com/)<br />-   [SharePoint 开发人员中心](/sharepoint/dev/)<br />-   [SharePoint Server 开发人员中心](/previous-versions/office/fp161348\(v\=office.15\))<br />-   [SharePoint Designer 开发人员中心](/previous-versions/office/fp161348\(v\=office.15\))<br />-   [ASP.NET 开发人员中心](https://msdn.microsoft.com/aa336522.aspx)|
|![提供反馈](../sharepoint/media/vs-icon-feedback.gif "提供反馈")|**提供反馈**<br /><br /> 提供有关 Visual Studio 的反馈：<br /><br /> -   [Microsoft Connect](http://go.microsoft.com/fwlink/?LinkID=150463)<br /><br /> 提供有关 Visual Studio 文档的反馈：<br /><br /> -   **轻量级视图。** 如果位于任意主题的顶部，可以选择“评估该主题”  链接来跳转到该主题的底部，在这里你可以指定“是”  或“否”  来对  “你是否认为本主题有用?”作出响应然后，你可以选择一个或多个复选框（选择“否” 后出现的），在文本框中或两者中提供详细信息。 完成后，选择“提交”  按钮。<br />-   **无脚本视图。** 在本主题的顶部，选择**反馈**链接以在 TechNet 和表达式库反馈论坛中提供反馈。<br />-   **经典视图。** 在该主题顶部，选择“反馈”  图标，以向文档团队提供关于该主题的反馈。|
