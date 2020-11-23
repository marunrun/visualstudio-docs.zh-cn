---
title: 创建 SharePoint 工作流解决方案 | Microsoft Docs
description: 使用工具创建 SharePoint 工作流解决方案，进而创建在 SharePoint 网站中管理文档生命周期和列出项目的自定义工作流。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: dd3f88df661537434c79a8b0049f90ddbce14c70
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850606"
---
# <a name="create-sharepoint-workflow-solutions"></a>创建 SharePoint 工作流解决方案

[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 提供了工具来帮助创建自定义工作流，从而管理 SharePoint 网站中文档和列表项的生命周期。 提供的项包括设计器、一组活动控件以及必需的程序集引用。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 还包括 SharePoint 自定义向导，它可帮助创建和配置工作流。

有关 SharePoint 的详细信息，请参阅 [Microsoft SharePoint 产品和技术](/sharepoint/dev/)。

## <a name="workflows-in-sharepoint"></a>SharePoint 中的工作流
 向 SharePoint 库或列表添加工作流时，会对库或列表中的所有项强制执行业务流程。 工作流描述了系统或用户必须对每个项目执行的操作，例如发送要编辑再评审的项目。 这些操作被称为“活动”，是工作流的构建基块。

 可在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中创建 SharePoint 工作流并将其部署到 SharePoint 网站。 将工作流部署到 SharePoint 后，可将其与库或列表关联。 然后，它可由某个进程自动启动，也可由用户手动启动。 有关工作流操作的详细信息，请参阅[使用 Visual Studio 开发 SharePoint 工作流](/sharepoint/dev/general-development/develop-sharepoint-workflows-using-visual-studio)。

## <a name="create-custom-sharepoint-workflows"></a>创建自定义 SharePoint 工作流
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中提供两个 SharePoint 工作流项目：顺序工作流和状态机工作流 。

 顺序工作流表示一系列步骤。 这些步骤会逐个执行，直到最后一个活动完成。 顺序工作流始终严格按顺序执行。 它们可接收外部事件并包括并行逻辑流，因此执行的确切顺序可能会有所不同。 下图显示了一个顺序工作流的示例。

 ![顺序工作流](../sharepoint/media/sp-sequential.png "顺序工作流")

 状态机工作流表示一组状态、转换和操作。 状态机工作流中的步骤以异步方式执行。 这意味着它们不一定要逐个执行，而是由动作和状态触发。 将一个状态指定为开始状态，然后根据事件转换到另一个状态。 状态机可具有确定工作流结束的最终状态。 下图显示了一个状态机工作流的示例。

 ![状态机工作流](../sharepoint/media/sp-state.png "状态机工作流")

 有关工作流类型的详细信息，请参阅[工作流类型](/previous-versions/office/developer/sharepoint-2010/ms468447(v=office.14))。

### <a name="use-the-wizard"></a>使用向导
 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中创建 SharePoint 工作流项目时，请先在 SharePoint 自定义向导中指定其设置。 向导使用这些设置在解决方案资源管理器中创建一个项目。 此项目包含一个代码文件、几个用于部署工作流的文件，以及对创建自定义 SharePoint 工作流所需的程序集的引用。

 创建工作流后，可在“属性”窗口中修改其属性。 尽管大多数工作流属性都可在“属性”窗口中直接更改，但有些属性要求单击省略号按钮（![ASP.NET 移动设计器中的省略号](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")）才能更改其值。 此按钮将重启 SharePoint 自定义向导。 进行属性值更改后，选择“完成”按钮来完成更改。

> [!NOTE]
> “工作流类型”属性只读且不能更改。 如果要更改工作流类型，必须再创建一个工作流。

## <a name="design-a-sharepoint-workflow"></a>设计 SharePoint 工作流
 定义业务流程中的所有步骤之后，请使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 工作流设计器来设计 SharePoint 工作流。 若要打开设计器，请在解决方案资源管理器中双击 Workflow1.cs 或 Workflow1.vb，或者打开这些文件的快捷菜单，然后选择“打开” 。

### <a name="activities"></a>活动
 若要设计工作流，请将活动从“工具箱”添加到设计器上的“工作流计划”。 工作流计划包含按应执行的顺序排列的活动序列。

 有两种类型的活动：

- 简单活动执行单个工作单元，例如“延迟 1 天”或“启动 Web 服务”。

- 复合活动包含其他活动；例如，条件活动可能包含两个分支。

  “工具箱”中提供了这两种类型的活动。

  活动可具有属性、方法和事件。 使用“属性”窗口设置活动的属性。

  还可创建自定义活动。 有关详细信息，请参见[演练：创建自定义站点工作流活动](../sharepoint/walkthrough-create-a-custom-site-workflow-activity.md)。

  活动在“工具箱”的以下选项卡中进行整理：

- SharePoint 工作流

- Windows 工作流 v3.0

- Windows 工作流 v3.5

  并非所有核心工作流活动都受到 SharePoint 支持。 有关详细信息，请参阅 [Windows SharePoint Services 的工作流活动概述](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14))。

#### <a name="sharepoint-workflow-activities"></a>SharePoint 工作流活动
 “SharePoint 工作流”选项卡包含在 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 中使用的专用活动。 这些活动简化了文档生命周期工作流的开发。 要详细了解“SharePoint 工作流”选项卡中列出的活动，请参阅 [Windows SharePoint Services 的工作流活动概述](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14))。

#### <a name="windows-workflow-activities"></a>Windows 工作流活动
 “Windows 工作流”选项卡包含 [!INCLUDE[TLA#tla_workflow](../sharepoint/includes/tlasharptla-workflow-md.md)] 提供的活动。 可使用这些活动为任何类型的 Windows 工作流应用程序创建工作流计划。

 要详细了解“Windows 工作流”选项卡中列出的活动，请参阅 [Windows Workflow Foundation 活动](/previous-versions/dotnet/netframework-3.5/ms733615(v=vs.90))。 有关 Windows Workflow Foundation 的详细信息，请参阅 [Windows Workflow Foundation 概述](/previous-versions/dotnet/netframework-3.5/ms734631(v=vs.90))。

### <a name="work-with-activities-in-the-designer"></a>处理设计器中的活动
 工作流计划可包含 Windows 工作流活动和 SharePoint 工作流活动的组合。

 设计器显示视觉提示，帮助你正确定位和配置活动。 当您将活动拖动或复制到工作流时间表上时，设计器会显示绿色加号 (+) 图标，为您指示该活动在工作流中的有效位置。 不能将活动放置在会使其无效的位置。 例如，不能将“发送”活动定位为“侦听”活动分支中的第一个活动。 有关详细信息，请参阅 [SharePoint Designer 开发人员中心](https://developer.microsoft.com/office/docs)。

## <a name="collect-information-during-the-workflow"></a>在工作流期间收集信息
 你可能想要在工作流中的预定义时间收集用户的信息。 可使用窗体或项属性来收集信息。

### <a name="forms"></a>窗体
 窗体类似于对话框，它包含问题并为用户提供答题方式。

 可在工作流中使用 4 种类型的窗体：

- 关联

- 启动

- 修改

- 任务

  其中，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 包括关联和启动窗体的项模板。 关联窗体的一个示例是允许安装工作流的管理员输入与工作流相关的参数，例如支出工作流的支出限制。 启动窗体的一个示例是允许支出工作流的用户将支出金额输入工作流。 有关这些窗体类型的详细信息，请参阅 [SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

### <a name="item-properties"></a>项属性
 你还可使用 SharePoint 库或列表中项的属性来收集用户的信息。 主代码文件（Workflow1.cs 或 Workflow1.vb）声明了名为 `workflowProperties` 的 Microsoft.SharePoint.Workflow.SPWorkflowActivationProperties.WorkflowProperties 类的实例。 使用 `workflowProperties` 对象在代码中访问库或列表的属性。 有关示例，请参阅[演练：创建和调试 SharePoint 工作流解决方案](../sharepoint/walkthrough-creating-and-debugging-a-sharepoint-workflow-solution.md)。

## <a name="debug-a-sharepoint-workflow-template"></a>调试 SharePoint 工作流模板
 可像调试其他 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 基于 Web 的项目一样调试 SharePoint 工作流项目。 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 调试器时，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 使用在 SharePoint 自定义向导中指定的设置打开相应的 SharePoint 网站，并将工作流模板与相应的库或列表自动关联。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 还将 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 调试程序附加到名为 w3wp.exe 的 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 进程。

 若要测试工作流，必须手动启动它。 有关详细信息，请参阅[调试 SharePoint 解决方案](../sharepoint/debugging-sharepoint-solutions.md)中的“调试工作流”部分。 要详细了解 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Web 应用程序调试，请参阅[调试 Web 应用程序和脚本](../debugger/how-to-enable-debugging-for-aspnet-applications.md)。

## <a name="deploy-a-sharepoint-workflow-template"></a>部署 SharePoint 工作流模板
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint 工作流项目的部署方式与其他 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint 项目相同。 有关详细信息，请参阅[打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)。

## <a name="import-globally-reusable-workflows"></a>导入全局可重用工作流
 除了创建特定于站点的可重用工作流外，使用 SharePoint Designer 还可创建全局可重用工作流，这些工作流可由任何 SharePoint 网站使用。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的“导入可重用工作流”项目当前不导入全局可重用工作流。 但是，你可使用 SharePoint Designer 将全局可重用工作流转换为可重用工作流，或者将工作流导入为未转换的声明性工作流。 有关详细信息，请参阅[从现有的 SharePoint 网站导入项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[演练：创建和调试 SharePoint 工作流解决方案](../sharepoint/walkthrough-creating-and-debugging-a-sharepoint-workflow-solution.md)|逐步指导你创建和调试简单的 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 工作流。|
|[演练：使用关联和启动窗体创建工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)|逐步指导你创建具有关联和启动窗体的功能更完备的 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 工作流。|
|[演练：将应用程序页添加到工作流](../sharepoint/walkthrough-add-an-application-page-to-a-workflow.md)|基于[演练：创建具有关联和启动窗体的工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)主题，方式是添加一个附加的 .aspx 应用程序页，它会报告输入到工作流中的数据。|
|[演练：创建自定义站点工作流活动](../sharepoint/walkthrough-create-a-custom-site-workflow-activity.md)|演示如何执行两项关键任务：创建网站级工作流和创建自定义工作流活动。|
|[演练：将 SharePoint Designer 可重用工作流导入 Visual Studio](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)|演示如何将在 SharePoint Designer 2010 中创建的可重用声明性工作流导入到 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint 项目中。|

## <a name="see-also"></a>请参阅

- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)