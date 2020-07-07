---
title: 创建 SharePoint 工作流解决方案 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
f1_keywords:
- VSTO.NewSharePointWorkflowWizard.Page3
- VS.SharePointTools.Workflow.WorkflowName
- VSTO.NewSharePointWorkflowWizard.Page2
- VSTO.NewSharePointWorkflowWizard.Page1
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2c787009577735213437140513ec095f81c3f43b
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015284"
---
# <a name="create-sharepoint-workflow-solutions"></a>创建 SharePoint 工作流解决方案

[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]提供的工具可帮助您创建自定义工作流，用于管理 SharePoint 网站中文档和列表项的生命周期。 提供的项包括设计器、一组活动控件以及必需的程序集引用。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]还包括**SharePoint 自定义向导**，用于帮助创建和配置工作流。

有关 SharePoint 的详细信息，请参阅[Microsoft Sharepoint 产品和技术](/sharepoint/dev/)。

## <a name="workflows-in-sharepoint"></a>SharePoint 中的工作流
 向 SharePoint 库或列表中添加工作流时，会对库或列表中的所有项强制执行业务流程。 工作流描述系统或用户必须对每个项执行的操作，例如，发送要编辑的项，然后查看。 这些操作称为*活动*，是工作流的构建基块。

 你可以在中创建 SharePoint 工作流 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，并将其部署到 sharepoint 网站。 将工作流部署到 SharePoint 后，可将其与库或列表相关联。 然后，它可以由某个进程自动启动，也可以由用户手动启动。 有关工作流操作的详细信息，请参阅[使用 Visual Studio 开发 SharePoint 工作流](/sharepoint/dev/general-development/develop-sharepoint-workflows-using-visual-studio)。

## <a name="create-custom-sharepoint-workflows"></a>创建自定义 SharePoint 工作流
 中提供了两个 SharePoint 工作流项目 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ：**顺序工作流**和**状态机工作流**。

 *顺序工作流*表示一系列步骤。 将逐个执行这些步骤，直到最后一个活动完成。 顺序工作流始终严格按顺序执行。 由于它们可以接收外部事件，并包括并行逻辑流，因此执行的准确顺序可能会有所不同。 下图显示了顺序工作流的示例。

 ![顺序工作流](../sharepoint/media/sp-sequential.png "顺序工作流")

 *状态机工作流*表示一组状态、转换和操作。 状态机工作流中的步骤以异步方式执行。 这意味着它们不一定再执行一次，而是由操作和状态触发。 将一个状态指定为开始状态，然后，根据事件，将转换为另一种状态。 状态机可以具有确定工作流结束的最终状态。 下图显示了状态机工作流的示例。

 ![状态机工作流](../sharepoint/media/sp-state.png "状态机工作流")

 有关工作流类型的详细信息，请参阅[工作流类型](/previous-versions/office/developer/sharepoint-2010/ms468447(v=office.14))。

### <a name="use-the-wizard"></a>使用向导
 当您在中创建 SharePoint 工作流项目时 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，您首先在 " **SharePoint 自定义向导**" 中指定其设置。 向导使用这些设置在**解决方案资源管理器**中创建项目。 此项目包含代码文件、用于部署工作流的多个文件以及对创建自定义 SharePoint 工作流所需的程序集的引用。

 创建工作流后，可以在属性窗口中修改其属性。 尽管大部分工作流属性都可以直接在属性窗口中进行更改，但某些属性要求您单击省略号按钮（![ASP.NET Mobile 设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")）以更改其值。 此按钮重新启动**SharePoint 自定义向导**。 更改属性值后，选择 "**完成**" 按钮以完成更改。

> [!NOTE]
> **工作流类型**属性是只读的，无法更改。 如果要更改工作流类型，则必须创建另一个工作流。

## <a name="design-a-sharepoint-workflow"></a>设计 SharePoint 工作流
 定义业务流程中的所有步骤后，请使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 工作流设计器来设计 SharePoint 工作流。 若要打开设计器，请在**解决方案资源管理器**中双击 "Workflow1.cs" 或 "workflow1.xaml"，或打开其中一个文件的快捷菜单，然后选择 "**打开**"。

### <a name="activities"></a>活动
 若要设计工作流，请将 "**工具箱**" 中的活动添加到设计器中的*工作流计划*。 工作流计划包含按应执行的顺序排列的活动序列。

 有两种类型的活动：

- *简单活动*执行单个工作单元，如 "延迟1天" 或 "启动 Web 服务"。

- *复合活动*包含其他活动;例如，条件活动可能包含两个分支。

  **工具箱**中提供了这两种类型的活动。

  活动可以具有属性、方法和事件。 使用 "**属性**" 窗口设置活动的属性。

  您还可以创建自定义活动。 有关详细信息，请参阅[演练：创建自定义站点工作流活动](../sharepoint/walkthrough-create-a-custom-site-workflow-activity.md)。

  活动组织在**工具箱**中的以下选项卡中：

- **SharePoint 工作流**

- **Windows Workflow 3。0**

- **Windows Workflow 3。5**

  SharePoint 不支持所有核心工作流活动。 有关详细信息，请参阅[Windows SharePoint Services 的工作流活动概述](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14))。

#### <a name="sharepoint-workflow-activities"></a>SharePoint 工作流活动
 " **SharePoint 工作流**" 选项卡包含在中使用的专用活动 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 。 这些活动简化并简化了文档生命周期工作流的开发。 有关 " **SharePoint 工作流**" 选项卡中列出的活动的详细信息，请参阅[Windows SharePoint Services 的工作流活动概述](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14))。

#### <a name="windows-workflow-activities"></a>Windows 工作流活动
 **Windows 工作流**选项卡包含由提供的活动 [!INCLUDE[TLA#tla_workflow](../sharepoint/includes/tlasharptla-workflow-md.md)] 。 您可以使用这些活动为任何类型的 Windows 工作流应用程序创建工作流计划。

 有关 " **Windows 工作流**" 选项卡中列出的活动的详细信息，请参阅[Windows Workflow Foundation 活动](/previous-versions/dotnet/netframework-3.5/ms733615(v=vs.90))。 有关 Windows Workflow Foundation 的详细信息，请参阅[Windows Workflow Foundation 概述](/previous-versions/dotnet/netframework-3.5/ms734631(v=vs.90))。

### <a name="work-with-activities-in-the-designer"></a>使用设计器中的活动
 工作流计划可以包含 Windows 工作流活动和 SharePoint 工作流活动的组合。

 设计器将显示可视提示，以帮助您正确定位和配置活动。 当您将活动拖动或复制到工作流时间表上时，设计器会显示绿色加号 (+) 图标，为您指示该活动在工作流中的有效位置。 不能将活动放置在不有效的位置。 例如，您不能将发送活动定位为 "侦听" 活动分支中的第一个活动。 有关详细信息，请参阅[SharePoint Designer 开发人员中心](https://developer.microsoft.com/office/docs)。

## <a name="collect-information-during-the-workflow"></a>在工作流过程中收集信息
 您可能想要在工作流中的预定义时间收集用户的信息。 您可以使用窗体或项属性来收集信息。

### <a name="forms"></a>窗体
 窗体类似于包含问题的对话框，并为用户提供了回答答案的方式。

 可在工作流中使用四种类型的窗体：

- 关联

- 初始

- 修改

- 任务

  其中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 包括关联窗体和启动窗体的项模板。 *关联窗体*的一个示例是允许管理员安装工作流的输入与工作流相关的参数，如支出工作流的支出限制。 *启动窗体*的一个示例就是让费用工作流的用户将其投入到工作流中的量。 有关这些类型的窗体的详细信息，请参阅[SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

### <a name="item-properties"></a>项属性
 你还可以通过使用 SharePoint 库或列表中项的属性来收集用户的信息。 主代码文件（Workflow1.cs 或 Workflow1.xaml）声明名为的 SPWorkflowActivationProperties 类的一个 `workflowProperties` 实例。 使用 `workflowProperties` 对象可通过代码访问库或列表的属性。 有关示例，请参阅[演练：创建和调试 SharePoint 工作流解决方案](../sharepoint/walkthrough-creating-and-debugging-a-sharepoint-workflow-solution.md)。

## <a name="debug-a-sharepoint-workflow-template"></a>调试 SharePoint 工作流模板
 调试 SharePoint 工作流项目的方式与调试其他 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 基于 Web 的项目相同。 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 调试器时，将 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 使用你在**SharePoint 自定义向导**中指定的设置打开相应的 sharepoint 网站并自动将工作流模板与相应的库或列表关联。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]还会将 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 调试器附加到 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 名为*w3wp.exe*的进程。

 若要测试工作流，必须手动启动它。 有关详细信息，请参阅[调试 SharePoint 解决方案](../sharepoint/debugging-sharepoint-solutions.md)中的 "调试工作流" 一节。 有关 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Web 应用程序调试的详细信息，请参阅[调试 web 应用程序和脚本](../debugger/how-to-enable-debugging-for-aspnet-applications.md)。

## <a name="deploy-a-sharepoint-workflow-template"></a>部署 SharePoint 工作流模板
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]SharePoint 工作流项目的部署与其他 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] sharepoint 项目一样。 有关详细信息，请参阅[打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)。

## <a name="import-globally-reusable-workflows"></a>导入全局可重用工作流
 除了创建特定于站点的可重用工作流，SharePoint Designer 还允许您创建可供任何 SharePoint 站点使用的*全局可重用工作流*。 当前中的 "导入可重用工作流" 项目 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 不会导入全局可重用工作流。 但是，可以使用 SharePoint Designer 将全局可重用工作流转换为可重用工作流，或将工作流导入为未转换的声明性工作流。 有关详细信息，请参阅[从现有 SharePoint 站点导入项目](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[演练：创建和调试 SharePoint 工作流解决方案](../sharepoint/walkthrough-creating-and-debugging-a-sharepoint-workflow-solution.md)|逐步引导您创建和调试一个简单的 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 工作流。|
|[演练：创建具有关联窗体和启动窗体的工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)|逐步引导您创建 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 具有关联和启动窗体的功能更全面的工作流。|
|[演练：向工作流添加应用程序页](../sharepoint/walkthrough-add-an-application-page-to-a-workflow.md)|主题演练：通过添加一个报表，其中包含与工作流中输入的数据相关的附加 *.aspx*应用程序页面，[创建具有关联和启动窗体的工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)。|
|[演练：创建自定义站点工作流活动](../sharepoint/walkthrough-create-a-custom-site-workflow-activity.md)|演示如何执行两项关键任务：创建网站级工作流，以及创建自定义工作流活动。|
|[演练：将 SharePoint Designer 可重用工作流导入 Visual Studio](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)|演示如何将在 SharePoint Designer 2010 中创建的可重用声明性工作流导入到 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint 项目中。|

## <a name="see-also"></a>另请参阅

- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)