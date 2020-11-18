---
title: 如何：创建应用程序页 |Microsoft Docs
description: 在 Visual Studio 中创建一个 ASP.NET 网页 (也称为应用程序页) 一个或多个 SharePoint 站点。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application pages [SharePoint development in Visual Studio], adding
- application pages [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: df52ca75ef99fe98158cb5f874e59fe4ee0c47b4
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2020
ms.locfileid: "94849852"
---
# <a name="how-to-create-an-application-page"></a>如何：创建应用程序页
  可以为一个或多个 SharePoint 网站创建 ASP.NET 网页。 在 SharePoint 中，这些页称为 "应用程序页"。 与网站页不同，应用程序页包含在该页后面运行的代码。 有关详细信息，请参阅 [为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)。

### <a name="to-create-an-application-page"></a>创建应用程序页

1. 在 Visual Studio 中打开或创建一个 SharePoint 项目。

     有关详细信息，请参阅 [SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

2. 在 **“解决方案资源管理器”** 中，选择项目节点。

3. 在菜单栏上，选择 "**项目**" "  >  **添加新项**"。

4. 在 " **添加新项** " 对话框中，展开 " **SharePoint** " 节点，然后选择 **2010** 项。

5. 在 SharePoint 模板列表中，选择 " **应用程序" 页**。

6. 在 " **名称** " 框中，指定应用程序页面的名称，然后选择 " **添加** " 按钮。

     Visual Studio 将多个文件夹和文件添加到你的项目。 有关这些文件的详细信息，请参阅 [为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)。

     在 Visual Web Developer 设计器的 " **源** " 视图中，将显示 "ASP.NET" 页文件。 可以通过从 " **工具箱** " 添加控件并将其放置在内容占位符上来设计页面。 有关详细信息，请参阅 ["源视图"、"网页设计器"](/previous-versions/aspnet/ms178154\(v\=vs.100\))。

7. 如果您要处理控件事件，请向应用程序页的代码文件添加代码。

     如果展开 ASP.NET 页面文件的节点并具有 *.cs* 或 *.vb* 扩展名（具体取决于项目的语言），则将显示该代码文件。 有关如何创建应用程序页的端到端示例，请参阅 [演练：创建 SharePoint 应用程序页](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)。

## <a name="see-also"></a>另请参阅
- [为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)
- [演练：创建 SharePoint 应用程序页](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)
