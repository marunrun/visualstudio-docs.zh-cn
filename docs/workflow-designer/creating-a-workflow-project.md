---
title: 创建基础工作流项目
ms.date: 06/25/2018
ms.topic: conceptual
helpviewer_keywords:
- Workflow Designer, creating a workflow project
- creating a workflow project
ms.assetid: 235a125e-ebe7-4a98-bf77-86c8558728fb
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e19ec88a4dec7a13ecc3d77e5d4fc1f04bb114bd
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66747802"
---
# <a name="workflow-project-templates"></a>工作流项目模板

可以使用 Visual Studio 项目模板来创建工作流、 Windows Communication Foundation (WCF) 工作流服务、 自定义活动和自定义活动设计器。 本文介绍如何使用 Visual Studio 中提供的项目模板创建库和应用程序。

## <a name="create-a-workflow-project"></a>创建工作流项目

Visual Studio 提供了四个不同的工作流项目模板：

- 工作流控制台应用程序

- WCF 工作流服务应用程序

- 活动库

- 活动设计器库

若要访问这些模板，请先安装**Windows Workflow Foundation**组件的 Visual Studio。 有关详细说明，请参阅[安装 Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)。

1. 安装后**Windows Workflow Foundation**组件，选择**文件** > **新建** > **项目**.

1. 搜索并选择工作流项目模板，例如，则**工作流控制台应用程序**模板。

1. 继续完成创建项目。

   > [!NOTE]
   > 如果你想要将新项目添加到现有解决方案，在 Visual Studio 中打开该解决方案中，右键单击该解决方案中的**解决方案资源管理器**，然后选择**添加** > **新建项目**。

## <a name="workflow-console-app"></a>工作流控制台应用程序

如果愿意**工作流控制台应用程序**模板，Visual Studio 在 XAML 中创建的工作流定义。 工作流设计器打开并显示你创建的工作流的画布。 若要编写工作流，将活动或其他工作流项从**工具箱**到设计图面。

## <a name="wcf-workflow-service-app"></a>WCF 工作流服务应用程序

如果愿意**WCF 工作流服务应用程序**模板，Visual Studio 将创建为 XAML 服务定义。 工作流设计器将打开到设计视图，其中<xref:System.Activities.Statements.Sequence>包含一组活动<xref:System.ServiceModel.Activities.Receive>和<xref:System.ServiceModel.Activities.SendReply>活动。

## <a name="activity-library"></a>活动库

如果愿意**活动库**模板，Visual Studio 在 XAML 中创建的活动定义。 工作流设计器打开并显示自定义活动的画布。 将从活动拖放**工具箱**到设计图面上要包含在自定义活动中。

> [!NOTE]
> 可以仅有一个子活动的自定义活动正文中。 但是，该子活动可以是复合活动，如<xref:System.Activities.Statements.Sequence>活动或<xref:System.Activities.Statements.Flowchart>活动。

## <a name="activity-designer-library"></a>活动设计器库

如果愿意**活动设计器库**模板，Visual Studio 创建一个活动设计器定义 XAML 和代码隐藏实现文件中。 工作流设计器打开并显示活动设计器的画布。 将 Windows Presentation Foundation (WPF) 控件从**工具箱**至设计图面上，若要在自定义活动设计器中使用它们。

有关如何实现自定义活动设计器的示例，请参阅[如何：创建自定义活动设计器](/dotnet/framework/windows-workflow-foundation/how-to-create-a-custom-activity-designer)。

> [!NOTE]
> 可以使用自定义活动设计器，自定义活动以及默认的.NET 活动。

## <a name="see-also"></a>请参阅

- [使用工作流设计器](developing-applications-with-the-workflow-designer.md)
- [设计工作流 (.NET Framework)](/dotnet/framework/windows-workflow-foundation/designing-workflows)