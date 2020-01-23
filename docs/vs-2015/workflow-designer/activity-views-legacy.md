---
title: 活动视图（旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- activities, activity views
- views, activity
- activity views
ms.assetid: 83dc68cd-2cb2-45c2-9a6e-10d82053171a
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7546f752ef7ee1053d1b0b785334a8da814720c6
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75851484"
---
# <a name="activity-views-legacy"></a>活动视图（旧版）
[!INCLUDE[wf](../includes/wf-md.md)] 提供的许多活动（可通过这些活动构成工作流）都具有旧 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 中可用的多个设计视图。 将活动设计器从 "**工具箱**" 拖动到设计图面上时，如果选择该活动，则可以通过使用 "**工作流**" 菜单或右键单击所选活动在不同的设计视图之间切换。 同时，当您将指针移到选定活动的名称上时，将出现一组以下拉方式显示的选项卡，可以用来在不同的视图之间切换。

 每个活动都至少有一个视图;这是将活动设计器从 "**工具箱**" 拖到设计图面上时显示的默认视图。 此活动默认视图作为菜单和选项卡上的 "**视图 [活动类型]** " 选项提供，例如 "**视图并行**"。 大多数活动都有附加视图，并且不同活动可以有不同的视图。 例如， [TransactionScopeActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.transactionscopeactivity.aspx)活动具有补偿视图，而[EventHandlingScopeActivity](https://msdn2.microsoft.com/library/system.workflow.activities.eventhandlingscopeactivity.aspx)活动具有事件视图。 Windows Workflow Foundation 附带的许多活动都有 "**查看取消处理程序**" 和 "**查看错误**" 设计视图，用于查看[CancellationHandlerActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.cancellationhandleractivity.aspx)和与其关联的[FaultHandlersActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.faulthandlersactivity.aspx) 。

 下表列出了每个视图的名称和说明。

|菜单/选项卡选项|描述|
|----------------------|-----------------|
|**视图 [活动类型]**|选择此菜单或选项卡选项可查看选定活动的默认图形表示形式。|
|**查看取消处理程序**|选择此菜单或选项卡选项视图可查看与选定活动关联的[CancellationHandlerActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.cancellationhandleractivity.aspx) 。|
|**查看错误处理程序**|选择此菜单或选项卡选项视图可查看与选定活动关联的[FaultHandlersActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.faulthandlersactivity.aspx) 。|
|**查看补偿处理程序**|选择此菜单或选项卡选项视图可查看与所选[TransactionScopeActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.transactionscopeactivity.aspx)关联的[CompensationHandlerActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.compensationhandleractivity.aspx) 。|
|**查看事件处理程序**|选择此菜单或选项卡选项视图可查看与所选[EventHandlingScopeActivity](https://msdn2.microsoft.com/library/system.workflow.activities.eventhandlingscopeactivity.aspx)关联的[EventHandlersActivity](https://msdn2.microsoft.com/library/system.workflow.activities.eventhandlersactivity.aspx) 。|

 有关类似视图的信息，请参阅[顺序工作流视图（旧版）](../workflow-designer/sequential-workflow-views-legacy.md)。

## <a name="see-also"></a>请参阅
 [旧版工作流活动](../workflow-designer/legacy-workflow-activities.md)[顺序工作流视图（旧版）](../workflow-designer/sequential-workflow-views-legacy.md)
