---
title: 顺序工作流视图（旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- sequential workflow views
- sequential workflows, views
ms.assetid: 135f24b9-1b37-442b-9ef8-f0f2108a3212
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 76d357c1f6ebc770d0e625e60bae237e37e0a6aa
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75846219"
---
# <a name="sequential-workflow-views-legacy"></a>顺序工作流视图（旧版）
[!INCLUDE[vs2010](../includes/vs2010-md.md)] 提供了一个可用于面向 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 或 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]的旧 [!INCLUDE[wfd1](../includes/wfd1-md.md)]。

 [!INCLUDE[wfd2](../includes/wfd2-md.md)]提供了一种以图形方式创建 [!INCLUDE[wf](../includes/wf-md.md)] 应用程序的方法（使用熟悉的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 用户界面）。 [!INCLUDE[wf](../includes/wf-md.md)] 应用程序由名为活动的工作流过程步骤组成。 若要创建工作流，请通过将活动设计器从 **"工具箱**" 拖动到设计图面上，在设计图面上撰写活动。

 创建一个[SequentialWorkflowActivity](https://msdn2.microsoft.com/library/system.workflow.activities.sequentialworkflowactivity.aspx)的顺序工作流时，可以使用工作流的三个视图。 可以从 "**工作流**" 菜单和设计图面上的上下文菜单中访问这些视图。

 下表列出了每个视图的名称和说明。

|菜单/选项卡选项|描述|
|----------------------|-----------------|
|**查看 SequentialWorkflow**|右键单击设计图面并从上下文菜单中选择 "**查看 SequentialWorkflow** " 选项以显示**顺序工作流**视图，该视图显示顺序工作流的基于活动的图形化表示形式。 或从 "**工作流**" 菜单中选择 "**查看 SequentialWorkflow** "。|
|**查看取消处理程序**|右键单击设计图面并从上下文菜单中选择 "**查看取消处理程序**" 选项以显示**顺序工作流**视图，该视图将显示与工作流关联的[CancellationHandlerActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.cancellationhandleractivity.aspx)活动。 或从 "**工作流**" 菜单中选择 "**查看取消处理程序**"。|
|**查看错误处理程序**|右键单击设计图面并从上下文菜单中选择 "**查看错误处理程序**" 选项以显示**错误**视图，其中显示了与工作流关联的[FaultHandlersActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.faulthandlersactivity.aspx)活动。 或从 "**工作流**" 菜单中选择 "**查看错误处理程序**"。|

 有关类似视图的详细信息，请参阅[活动视图（旧版）](../workflow-designer/activity-views-legacy.md)。

## <a name="see-also"></a>请参阅
 [活动视图（旧版）](../workflow-designer/activity-views-legacy.md) [创建旧工作流项目](../workflow-designer/creating-legacy-workflow-projects.md)[工作流创作模式](https://msdn2.microsoft.com/library/bb628440.aspx)
