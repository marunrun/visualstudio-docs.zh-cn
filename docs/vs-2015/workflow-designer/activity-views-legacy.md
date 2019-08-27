---
title: 活动视图 （旧版） |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 62b3c9185226512ff28c8d028cd0ba7d33b0f12f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977454"
---
# <a name="activity-views-legacy"></a>活动视图（旧版）
[!INCLUDE[wf](../includes/wf-md.md)] 提供的许多活动（可通过这些活动构成工作流）都具有旧 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 中可用的多个设计视图。 从活动设计器中拖动时**工具箱**拖到设计图面，并且之后每当选择该活动时，您可以通过使用不同的设计视图之间进行切换**工作流**菜单或通过右键单击选定的活动。 同时，当您将指针移到选定活动的名称上时，将出现一组以下拉方式显示的选项卡，可以用来在不同的视图之间切换。  
  
 每个活动都至少一个视图;这是从活动设计器中拖动时显示的默认视图**工具箱**拖到设计图面。 此活动默认视图是可用作**查看 [活动类型]** 上的菜单和选项卡上，例如，选项**查看 Parallel**。 大多数活动都有附加视图，并且不同活动可以有不同的视图。 例如， [TransactionScopeActivity](http://go.microsoft.com/fwlink?LinkID=65093)活动具有补偿视图和[EventHandlingScopeActivity](http://go.microsoft.com/fwlink?LinkID=65030)活动具有事件视图。 许多 Windows Workflow Foundation 附带的活动都有**查看取消处理程序**并**查看错误**设计视图，用于查看[CancellationHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65050)和一个[FaultHandlersActivity](http://go.microsoft.com/fwlink?LinkID=65055)与之关联。  
  
 下表列出了每个视图的名称和说明。  
  
|菜单/选项卡选项|描述|  
|----------------------|-----------------|  
|**查看 [活动类型]**|选择此菜单或选项卡选项可查看选定活动的默认图形表示形式。|  
|**查看取消处理程序**|选择此菜单或选项卡选项视图可查看[CancellationHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65050)与选定活动关联。|  
|**查看错误处理程序**|选择此菜单或选项卡选项视图可查看[FaultHandlersActivity](http://go.microsoft.com/fwlink?LinkID=65055)与选定活动关联。|  
|**查看补偿处理程序**|选择此菜单或选项卡选项视图可查看[CompensationHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65053)关联与所选[TransactionScopeActivity](http://go.microsoft.com/fwlink?LinkID=65093)。|  
|**查看事件处理程序**|选择此菜单或选项卡选项视图可查看[EventHandlersActivity](http://go.microsoft.com/fwlink?LinkID=65018)关联与所选[EventHandlingScopeActivity](http://go.microsoft.com/fwlink?LinkID=65030)。|  
  
 有关类似视图的信息，请参阅[顺序工作流视图 （旧版）](../workflow-designer/sequential-workflow-views-legacy.md)。  
  
## <a name="see-also"></a>请参阅  
 [旧版工作流活动](../workflow-designer/legacy-workflow-activities.md)   
 [顺序工作流视图（旧版）](../workflow-designer/sequential-workflow-views-legacy.md)