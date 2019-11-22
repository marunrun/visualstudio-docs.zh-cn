---
title: Using the Legacy State Machine Workflow Designer | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- StateFinalizationActivity activity
- StateActivity activity
- SetStateActivity activity
- EventDrivenActivity activity
- state machine workflow designer
- state machine workflows, designer
- state machine workflows, activities
- StateInitializationActivity activity
ms.assetid: 2cd21123-35c2-4eaf-82f6-86fce7a8f04d
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5bab07b8ba0b71bd880135518ff9ff5fc697d54c
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302805"
---
# <a name="using-the-legacy-state-machine-workflow-designer"></a>使用旧版状态机工作流设计器
When you are creating a new state machine workflow project in [!INCLUDE[vs2010](../includes/vs2010-md.md)] that targets either the [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] or the [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)], you can choose to use either the **State Machine Workflow Console Application** or the **State Machine Workflow Library** legacy project template. 如果选择其中一个状态机项目模板，则会以旧工作流设计器用户界面的形式呈现状态机设计器。 For information about the legacy state machine project templates, see [How to: Create State Machine Workflow Console Applications (Legacy)](../workflow-designer/how-to-create-state-machine-workflow-console-applications-legacy.md) and [How to: Create a State Machine Workflow Library (Legacy)](../workflow-designer/how-to-create-a-state-machine-workflow-library-legacy.md).

 状态机工作流由一组状态组成。 一个状态被指示为初始状态。 每个状态都可以接收一组特定事件。 视事件而定，可以转换到另一个状态。 状态机工作流可以有最终状态。 当转换到最终状态时，工作流将完成。

## <a name="state-machine-designer-views"></a>状态机设计器视图
 状态机设计器是一种自由形式的设计器，这意味着可以在设计图面上自由移动活动。 The state machine designer has two views: *state* view and *event-driven* view.

 状态视图显示状态活动和可包含在状态活动内的事件驱动的活动。 在此视图中，从一个状态到另一个状态的转换是由直线表示的，这些直线从一个状态中的事件驱动活动延伸到另一个状态。 也可以通过自己绘制直线来创建转换。 若要绘制转换，请选择事件驱动的活动，然后选择活动上的某个手柄并拖动该手柄。 此操作将绘制直线。 此直线随后将连接到目标状态，指示状态之间的转换。

 若要访问事件驱动的视图，请双击事件驱动的活动。 出现的设计器与顺序工作流设计器很像。 在设计器的顶部，导航栏显示直到所显示事件驱动活动为止的活动层次结构。 可以通过单击显示的层次结构中的任意元素导航回状态视图。 如果已在状态视图中绘制了从一个状态到另一个状态的转换，并且正在显示该活动的事件驱动视图，则会为您将一个已设置状态活动添加到事件驱动的活动。 如果更改已设置状态活动的属性，它将反映到状态视图中。

## <a name="state-machine-workflow-activities"></a>状态机工作流活动
 下表描述了状态机工作流设计器中使用的关键活动。

|工具箱名称|活动|描述|
|------------------|--------------|-----------------|
|**状态**|[StateActivity](https://go.microsoft.com/fwlink?LinkID=65042)|Represents a state in a state machine; may contain additional **StateActivity** activities. For more information, see [Using the StateActivity Activity](https://go.microsoft.com/fwlink?LinkID=65083).|
|**SetState**|[SetStateActivity](https://go.microsoft.com/fwlink?LinkID=65041)|指定到新状态的转换。 For more information, see [Using the SetStateActivity Activity](https://go.microsoft.com/fwlink?LinkID=65082).|
|**StateInitialization**|[StateInitializationActivity](https://go.microsoft.com/fwlink?LinkID=65044)|在进入某个状态时执行；可能包含其他活动。 For more information, see [Using the StateInitialization Activity](https://go.microsoft.com/fwlink?LinkID=65006).|
|**StateFinalization**|[StateFinalizationActivity](https://go.microsoft.com/fwlink?LinkID=65043)|Executes contained activities when leaving a [StateActivity](https://go.microsoft.com/fwlink?LinkID=65042) activity. For more information, see [Using the StateFinalizationActivity Activity](https://go.microsoft.com/fwlink?LinkID=65008).|
|**EventDriven**|[EventDrivenActivity](https://go.microsoft.com/fwlink?LinkID=65029)|用于依赖于外部事件开始执行的状态。 The **EventDrivenActivity** activity must have an activity that implements the [IEventActivity](https://go.microsoft.com/fwlink?LinkID=65032) interface as the first child activity. For more information, see [Using the EventDrivenActivity Activity](https://go.microsoft.com/fwlink?LinkID=65068).|

 The main component in a state machine workflow is the [StateActivity](https://go.microsoft.com/fwlink?LinkID=65042) activity. 在状态机工作流中的不同位置捕获了事件时，将会进入不同的状态，以处理与这些事件关联的任务。 在工作流的生存期内，工作流可能会离开和进入若干不同的状态。 These states connect to each other by using the [SetStateActivity](https://go.microsoft.com/fwlink?LinkID=65041) activity.

 When you drag a new **StateActivity** onto the workflow design surface, you can add [EventDrivenActivity](https://go.microsoft.com/fwlink?LinkID=65029), [StateInitializationActivity](https://go.microsoft.com/fwlink?LinkID=65044), [StateFinalizationActivity](https://go.microsoft.com/fwlink?LinkID=65043), or additional **StateActivity** activities as child activities.

> [!CAUTION]
> When you use the state machine workflow designer to create workflows, you must monitor the structure of the workflow you are designing with the **Document Outline** view window. The view of the structure of the state machine workflow in the **Document Outline** view window mirrors the logical layout of the activities in the workflow markup file. 工作流活动显示在设计图面上的物理布局可能不会反映工作流标记文件中活动的逻辑布局。
>
> To open the **Document Outline** window, on the **View** menu, point to **Other Windows**, and then select **Document Outline**.

## <a name="see-also"></a>请参阅
 [How to: Create State Machine Workflow Console Applications (Legacy)](../workflow-designer/how-to-create-state-machine-workflow-console-applications-legacy.md) [How to: Create a State Machine Workflow Library (Legacy)](../workflow-designer/how-to-create-a-state-machine-workflow-library-legacy.md) [State Machine Workflows](https://go.microsoft.com/fwlink?LinkID=65016) [Using the StateActivity Activity](https://go.microsoft.com/fwlink?LinkID=65083) [Using the StateInitializationActivity Activity](https://go.microsoft.com/fwlink?LinkID=65006) [Using the StateFinalizationActivity Activity](https://go.microsoft.com/fwlink?LinkID=65008) [Using the SetStateActivity Activity](https://go.microsoft.com/fwlink?LinkID=65082) [Using the EventDrivenActivity Activity](https://go.microsoft.com/fwlink?LinkID=65068)