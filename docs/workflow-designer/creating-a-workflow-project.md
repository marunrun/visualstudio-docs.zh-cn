---
title: 创建 Workflow Foundation 项目
ms.date: 06/25/2018
ms.topic: conceptual
helpviewer_keywords:
- Workflow Designer, creating a workflow project
- creating a workflow project
ms.assetid: 235a125e-ebe7-4a98-bf77-86c8558728fb
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f793e6ff468bdec6df499c5e5eb6b8524e9e4d5a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650579"
---
# <a name="workflow-project-templates"></a>工作流项目模板

可以通过使用 Visual Studio 项目模板来创建工作流、Windows Communication Foundation （WCF）工作流服务、自定义活动和自定义活动设计器。 本文介绍如何使用 Visual Studio 中提供的项目模板创建库和应用程序。

## <a name="create-a-workflow-project"></a>创建工作流项目

Visual Studio 提供了四种不同的工作流项目模板：

- 工作流控制台应用

- WCF 工作流服务应用

- 活动库

- 活动设计器库

若要访问这些模板，请首先安装 Visual Studio 的**Windows Workflow Foundation**组件。 有关详细说明，请参阅[安装 Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)。

1. 安装**Windows Workflow Foundation**组件后，选择 "**文件**"  >  "**新建** > **项目**"。

1. 搜索并选择一个工作流项目模板，例如 "**工作流控制台应用程序**" 模板。

1. 继续创建项目。

   > [!NOTE]
   > 如果要向现有解决方案中添加新项目，请在 Visual Studio 中打开该解决方案，在**解决方案资源管理器**中右键单击该解决方案，然后选择 "**添加** > "**新建项目**"。

## <a name="workflow-console-app"></a>工作流控制台应用

如果选择 "**工作流控制台应用程序**" 模板，Visual Studio 将在 XAML 中创建一个工作流定义。 工作流设计器将打开并显示所创建工作流的画布。 若要编写工作流，请将活动或其他工作流项从**工具箱**拖到设计图面。

## <a name="wcf-workflow-service-app"></a>WCF 工作流服务应用

如果选择 " **WCF 工作流服务应用程序**" 模板，Visual Studio 会将服务定义创建为 XAML。 工作流设计器将打开 "设计" 视图，其中包含一组 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动的 <xref:System.Activities.Statements.Sequence> 活动。

## <a name="activity-library"></a>活动库

如果选择 "**活动库**" 模板，Visual Studio 将在 XAML 中创建一个活动定义。 工作流设计器将打开并显示自定义活动的画布。 将活动从**工具箱**拖到设计图面上，以将其包含在您的自定义活动中。

> [!NOTE]
> 在自定义活动的主体中，只允许使用一个子活动。 但是，该子活动可以是复合活动，如 <xref:System.Activities.Statements.Sequence> 活动或 <xref:System.Activities.Statements.Flowchart> 活动。

## <a name="activity-designer-library"></a>活动设计器库

如果选择 "**活动设计器库**" 模板，则 Visual Studio 将在 XAML 中创建一个活动设计器定义，并在代码分离实现文件中创建。 工作流设计器随即打开并显示活动设计器的画布。 将 Windows Presentation Foundation （WPF）控件从**工具箱**拖到设计图面以在您的自定义活动设计器中使用它们。

有关如何实现自定义活动设计器的示例，请参阅[如何：创建自定义活动设计器](/dotnet/framework/windows-workflow-foundation/how-to-create-a-custom-activity-designer)。

> [!NOTE]
> 自定义活动设计器可用于自定义活动和默认的 .NET 活动。

## <a name="see-also"></a>请参阅

- [使用工作流设计器](developing-applications-with-the-workflow-designer.md)
- [设计工作流（.NET Framework）](/dotnet/framework/windows-workflow-foundation/designing-workflows)