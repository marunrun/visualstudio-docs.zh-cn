---
title: 为 Web 部件或应用程序页创建可重用控件 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
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
ms.openlocfilehash: b174e1e16802838f19cec6dce727ea3199df730f
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015146"
---
# <a name="create-reusable-controls-for-web-parts-or-application-pages"></a>为 web 部件或应用程序页创建可重用控件
  在 Visual Studio 中，你可以创建可由 SharePoint 中运行的应用程序页和 Web 部件使用的自定义可重用控件。 这些控件称为用户控件。 用户控件是一种类似于 ASP.NET 网页的复合控件，可以将现有 Web 服务器控件和标记添加到用户控件，并定义控件的属性和方法。 然后，你可以将它们嵌入到 ASP.NET 的网页中，它们作为一个单元。

## <a name="create-a-user-control"></a>创建用户控件
 若要创建用户控件，请将**用户控件**添加到**空 SharePoint 项目**。 有关详细信息，请参阅[如何：为 SharePoint 应用程序页或 web 部件创建用户控件](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)。

 添加**用户控件**项时，Visual Studio 会在项目中创建一个文件夹，然后将多个文件添加到该文件夹中。 下表对每个文件进行了说明。

|文件|说明|
|----------|-----------------|
|用户控件文件|定义用户控件。 通过向此文件添加控件和标记来设计用户控件。|
|代码文件|包含用户控件后的代码。 添加用于处理此文件事件的代码。|
|设计器代码文件|包含由设计器生成的代码，不应直接编辑。|

## <a name="design-the-user-control"></a>设计用户控件
 使用 Visual Studio 中的 Visual Web Developer 设计器设计用户控件。 当您在项目中打开用户控件文件并选择 "**设计**" 选项卡时，将显示此设计器。

## <a name="consume-the-user-control"></a>使用用户控件
 在应用程序页或 Web 部件中包含用户控件之前，这些控件不会显示在 SharePoint 中。

 若要在应用程序页中包含用户控件，请打开要向其中添加 ASP.NET 用户控件的网页。 切换到设计视图，然后在解决方案资源管理器中选择自定义用户控件文件，然后将其拖到页面上。 ASP.NET 用户控件将添加到页面中，并且设计器将创建 @ Register 指令，该指令是页识别用户控件所必需的。 你现在可以使用控件的公共属性和方法。

 若要在 Web 部件中包含用户控件，请将用户控件添加到 Web 部件 <xref:System.Web.UI.WebControls.WebParts.Part.Controls%2A> 代码文件中的 Web 部件集合。 下面的示例将用户控件添加到 <xref:System.Web.UI.WebControls.WebParts.Part.Controls%2A> Web 部件的集合中。

 [!code-vb[SP_VisualWebPart#5](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1.vb#5)]
 [!code-csharp[SP_VisualWebPart#5](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1.cs#5)]

## <a name="debug-a-user-control"></a>调试用户控件
 若要调试用户控件，请确保用户控件包含在 SharePoint 项目的应用程序页或 Web 部件中。 然后，你可以在用户控件中调试代码，就像调试任何 Visual Studio 项目中的代码一样。

 当你启动 Visual Studio 调试器时，Visual Studio 将打开 SharePoint 站点。

 在 SharePoint 中，打开包含用户控件的应用程序页。 如果用户控件包括在 Web 部件中，请将 Web 部件添加到 SharePoint 中的 Web 部件页。

 有关调试 SharePoint 项目的详细信息，请参阅[排查 sharepoint 解决方案问题](../sharepoint/troubleshooting-sharepoint-solutions.md)。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[如何：为 SharePoint 应用程序页或 web 部件创建用户控件](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)|演示如何创建可由在 SharePoint 中运行的应用程序页和 Web 部件使用的自定义的可重用控件。|
