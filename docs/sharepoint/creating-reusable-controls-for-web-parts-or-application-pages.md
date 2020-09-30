---
title: 为 Web 部件或应用程序页创建可重用控件 | Microsoft Docs
titleSuffix: ''
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
ms.openlocfilehash: d3052b2eab3dc353cdccc991a793c47485037fe8
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91585088"
---
# <a name="create-reusable-controls-for-web-parts-or-application-pages"></a>为 Web 部件或应用程序页创建可重用控件
  在 Visual Studio 中，你可以创建可由 SharePoint 中运行的应用程序页和 Web 部件使用的自定义可重用控件。 这些控件称为用户控件。 用户控件是一种复合控件，其工作原理与 ASP.NET 网页非常类似：可将现有 Web 服务器控件和标记添加到用户控件，并定义控件的属性和方法。 然后可以将它们嵌入到 ASP.NET 网页中，充当其中的一个单元。

## <a name="create-a-user-control"></a>创建用户控件
 若要创建用户控件，请将“用户控件”添加到“空白 SharePoint 项目” 。 有关详细信息，请参阅[如何：为 SharePoint 应用程序页或 Web 部件创建用户控件](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)。

 添加“用户控件”项时，Visual Studio 会在项目中创建一个文件夹，然后将多个文件添加到该文件夹中。 下表对每个文件进行了描述。

|文件|说明|
|----------|-----------------|
|用户控件文件|定义用户控件。 通过向此文件添加控件和标记来设计用户控件。|
|代码文件|包含用户控件背后的代码。 向此文件添加用于处理事件的代码。|
|设计器代码文件|包含设计器生成的代码，不应直接对其进行编辑。|

## <a name="design-the-user-control"></a>设计用户控件
 使用 Visual Studio 中的 Visual Web Developer 设计器设计用户控件。 在项目中打开用户控件文件并选择“设计”选项卡时，将显示此设计器。

## <a name="consume-the-user-control"></a>使用用户控件
 在应用程序页或 Web 部件中包含用户控件之前，这些控件不会显示在 SharePoint 中。

 若要在应用程序页中包含用户控件，请打开要向其添加 ASP.NET 用户控件的网页。 切换到设计视图，然后在解决方案资源管理器中选择自定义用户控件文件，并将其拖到页面上。 随即 ASP.NET 用户控件便添加到页面中，并且设计器将创建 @ Register 指令，这是页面识别用户控件所需的指令。 现在可以使用控件的公共属性和方法。

 若要在 Web 部件中包含用户控件，请将用户控件添加到 Web 部件代码文件中的 Web 部件 <xref:System.Web.UI.WebControls.WebParts.Part.Controls%2A> 集合中。 以下示例将用户控件添加到 Web 部件的 <xref:System.Web.UI.WebControls.WebParts.Part.Controls%2A> 集合中。

 [!code-vb[SP_VisualWebPart#5](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1.vb#5)]
 [!code-csharp[SP_VisualWebPart#5](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1.cs#5)]

## <a name="debug-a-user-control"></a>调试用户控件
 若要调试用户控件，请确保用户控件包含在 SharePoint 项目的应用程序页或 Web 部件中。 然后可在用户控件中调试代码，就像在任何 Visual Studio 项目中调试代码一样。

 当你启动 Visual Studio 调试器时，Visual Studio 将打开 SharePoint 网站。

 在 SharePoint 中，打开包含用户控件的应用程序页。 如果用户控件包含在 Web 部件中，请将 Web 部件添加到 SharePoint 中的 Web 部件页。

 有关调试 SharePoint 项目的详细信息，请参阅 [SharePoint 解决方案疑难解答](../sharepoint/troubleshooting-sharepoint-solutions.md)。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[如何：为 SharePoint 应用程序页或 Web 部件创建用户控件](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)|演示如何创建可由 SharePoint 中运行的应用程序页和 Web 部件使用的自定义可重用控件。|
