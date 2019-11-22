---
title: Activity Views (Legacy) | Microsoft Docs
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
ms.openlocfilehash: 9b65a46d5d0061eeaf3ad707affea1423e5fca5d
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297534"
---
# <a name="activity-views-legacy"></a>活动视图（旧版）
[!INCLUDE[wf](../includes/wf-md.md)] 提供的许多活动（可通过这些活动构成工作流）都具有旧 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 中可用的多个设计视图。 When you drag an activity designer from the **Toolbox** onto the design surface, and thereafter whenever you select the activity, you can switch between the different design views by using either the **Workflow** menu or by right-clicking the selected activity. 同时，当您将指针移到选定活动的名称上时，将出现一组以下拉方式显示的选项卡，可以用来在不同的视图之间切换。

 Every activity has at least one view; this is the default view shown when you drag an activity designer from the **Toolbox** onto the design surface. This activity default view is available as the **View [activity type]** option on the menus and tab, for example, **View Parallel**. 大多数活动都有附加视图，并且不同活动可以有不同的视图。 For example, the [TransactionScopeActivity](https://go.microsoft.com/fwlink?LinkID=65093) activity has the compensation view and the [EventHandlingScopeActivity](https://go.microsoft.com/fwlink?LinkID=65030) activity has an events view. Many of the activities that come with Windows Workflow Foundation have **View Cancel Handler** and **View Faults** design views to view the [CancellationHandlerActivity](https://go.microsoft.com/fwlink?LinkID=65050) and a [FaultHandlersActivity](https://go.microsoft.com/fwlink?LinkID=65055) associated with them.

 下表列出了每个视图的名称和说明。

|菜单/选项卡选项|描述|
|----------------------|-----------------|
|**View [activity type]**|选择此菜单或选项卡选项可查看选定活动的默认图形表示形式。|
|**View Cancel Handler**|Select this menu or tab option view to view the [CancellationHandlerActivity](https://go.microsoft.com/fwlink?LinkID=65050) associated with the selected activity.|
|**View Fault Handler**|Select this menu or tab option view to view the [FaultHandlersActivity](https://go.microsoft.com/fwlink?LinkID=65055) associated with the selected activity.|
|**View Compensation Handler**|Select this menu or tab option view to view the [CompensationHandlerActivity](https://go.microsoft.com/fwlink?LinkID=65053) associated with the selected [TransactionScopeActivity](https://go.microsoft.com/fwlink?LinkID=65093).|
|**View Events Handler**|Select this menu or tab option view to view the [EventHandlersActivity](https://go.microsoft.com/fwlink?LinkID=65018) associated with the selected the [EventHandlingScopeActivity](https://go.microsoft.com/fwlink?LinkID=65030).|

 For information about similar views, see [Sequential Workflow Views (Legacy)](../workflow-designer/sequential-workflow-views-legacy.md).

## <a name="see-also"></a>请参阅
 [Legacy Workflow Activities](../workflow-designer/legacy-workflow-activities.md) [Sequential Workflow Views (Legacy)](../workflow-designer/sequential-workflow-views-legacy.md)