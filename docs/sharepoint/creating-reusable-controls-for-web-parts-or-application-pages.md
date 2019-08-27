---
title: 为 Web 部件或应用程序页创建可重用控件 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- user controls [SharePoint development in Visual Studio], creating
- SharePoint development in Visual Studio, user controls
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 71e67ab41fd39563520370eb079fca1b7c82015e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62952784"
---
# <a name="create-reusable-controls-for-web-parts-or-application-pages"></a>创建 web 部件或应用程序页的可重用的控件
  在 Visual Studio 中，你可以创建可由 SharePoint 中运行的应用程序页和 Web 部件使用的自定义可重用控件。 这些控件称为用户控件。 用户控件是一种工作方式非常类似于 ASP.NET 网页的复合控件，可以将现有的 Web 服务器控件和标记添加到用户控件，并定义用于控制属性和方法。 您然后可以将它们嵌入在 ASP.NET Web 页面，其中作为一个单元中。

## <a name="create-a-user-control"></a>创建用户控件
 若要创建的用户控件，添加**用户控件**到**空 SharePoint 项目**。 有关详细信息，请参阅[如何：创建 SharePoint 应用程序页或 web 部件的用户控件](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)。

 当您将添加**用户控件**项，Visual Studio 在项目中，创建一个文件夹，然后将多个文件添加到的文件夹。 下表介绍每个文件。

|文件|描述|
|----------|-----------------|
|用户控件文件|定义用户控件。 通过将控件和标记添加到此文件中设计用户控件。|
|代码文件|包含代码隐藏用户控件。 添加代码以处理对此文件的事件。|
|设计器代码文件|包含设计器生成的代码，不应直接编辑。|

## <a name="design-the-user-control"></a>设计用户控件
 在 Visual Studio 中使用 Visual Web Developer 设计器设计用户控件。 此设计器将显示在项目中打开用户控件文件并选择**设计**选项卡。

## <a name="consume-the-user-control"></a>使用用户控件
 直到将其包含在应用程序页或 Web 部件在 SharePoint 中不显示用户控件。

 若要在应用程序页中包含用户控件，打开你想要添加 ASP.NET 用户控件的网页。 切换到设计视图中，然后在解决方案资源管理器，选择你的自定义用户控件文件并将其拖到绘图页上。 ASP.NET 用户控件添加到页上，并在设计器创建的 @ Register 指令，所需的页后，可以识别用户控件。 现在可以使用控件的公共属性和方法。

 若要在 Web 部件中包含用户控件，请将用户控件添加到 Web 部件<xref:System.Web.UI.WebControls.WebParts.Part.Controls%2A>Web 部件代码文件中的集合。 下面的示例添加到用户控件<xref:System.Web.UI.WebControls.WebParts.Part.Controls%2A>Web 部件的集合。

 [!code-vb[SP_VisualWebPart#5](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1.vb#5)]
 [!code-csharp[SP_VisualWebPart#5](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1.cs#5)]

## <a name="debug-a-user-control"></a>调试用户控件
 若要调试的用户控件，请确保用户控件包括在应用程序页或 Web 部件在 SharePoint 项目中。 然后可以调试在用户控件中的代码，就像就像调试任何 Visual Studio 项目中的代码。

 启动 Visual Studio 调试器时，Visual Studio 会打开 SharePoint 站点。

 在 SharePoint 中，打开包含用户控件的应用程序页。 如果用户控件包含在 Web 部件，将 Web 部件添加到 SharePoint 中的 Web 部件页。

 有关调试 SharePoint 项目的详细信息，请参阅[进行故障排除 SharePoint 解决方案](../sharepoint/troubleshooting-sharepoint-solutions.md)。

## <a name="related-topics"></a>相关主题

|标题|说明|
|-----------|-----------------|
|[如何：创建 SharePoint 应用程序页或 web 部件的用户控件](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)|演示如何创建可由应用程序页和在 SharePoint 中运行的 Web 部件使用的自定义可重用控件。|
