---
title: 使用旧状态机工作流设计器 |Microsoft Docs
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
ms.openlocfilehash: 77bb2c7abb49dbf6fe973ebc80f8340000e4afbd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "75846003"
---
# <a name="using-the-legacy-state-machine-workflow-designer"></a>使用旧版状态机工作流设计器
如果要在中创建新的状态机工作流项目， [!INCLUDE[vs2010](../includes/vs2010-md.md)] 该项目面向 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 或 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] ，则可以选择使用 " **状态机工作流" 控制台应用程序** 或 " **状态机工作流库** "。 如果选择其中一个状态机项目模板，则会以旧工作流设计器用户界面的形式呈现状态机设计器。 有关旧状态机项目模板的信息，请参阅 [如何：创建状态机工作流控制台应用程序 (旧) ](../workflow-designer/how-to-create-state-machine-workflow-console-applications-legacy.md) 和 [如何：创建状态机工作流库 (旧) ](../workflow-designer/how-to-create-a-state-machine-workflow-library-legacy.md)。

 状态机工作流由一组状态组成。 一个状态被指示为初始状态。 每个状态都可以接收一组特定事件。 视事件而定，可以转换到另一个状态。 状态机工作流可以有最终状态。 当转换到最终状态时，工作流将完成。

## <a name="state-machine-designer-views"></a>状态机设计器视图
 状态机设计器是一种自由形式的设计器，这意味着可以在设计图面上自由移动活动。 状态机设计器具有两个视图： " *状态* 视图" 和 " *事件驱动* 视图"。

 状态视图显示状态活动和可包含在状态活动内的事件驱动的活动。 在此视图中，从一个状态到另一个状态的转换是由直线表示的，这些直线从一个状态中的事件驱动活动延伸到另一个状态。 也可以通过自己绘制直线来创建转换。 若要绘制转换，请选择事件驱动的活动，然后选择活动上的某个手柄并拖动该手柄。 此操作将绘制直线。 此直线随后将连接到目标状态，指示状态之间的转换。

 若要访问事件驱动的视图，请双击事件驱动的活动。 出现的设计器与顺序工作流设计器很像。 在设计器的顶部，导航栏显示直到所显示事件驱动活动为止的活动层次结构。 可以通过单击显示的层次结构中的任意元素导航回状态视图。 如果已在状态视图中绘制了从一个状态到另一个状态的转换，并且正在显示该活动的事件驱动视图，则会为您将一个已设置状态活动添加到事件驱动的活动。 如果更改已设置状态活动的属性，它将反映到状态视图中。

## <a name="state-machine-workflow-activities"></a>状态机工作流活动
 下表描述了状态机工作流设计器中使用的关键活动。

|工具箱名称|活动|说明|
|------------------|--------------|-----------------|
|**状态**|[StateActivity](https://msdn2.microsoft.com/library/system.workflow.activities.stateactivity.aspx)|表示状态机中的状态;可能包含其他 **StateActivity** 活动。 有关详细信息，请参阅 [使用 StateActivity 活动](https://msdn2.microsoft.com/library/bb628612.aspx)。|
|**SetState**|[SetStateActivity](https://msdn2.microsoft.com/library/system.workflow.activities.setstateactivity.aspx)|指定到新状态的转换。 有关详细信息，请参阅 [使用 SetStateActivity 活动](https://msdn2.microsoft.com/library/bb628469.aspx)。|
|**StateInitialization**|[StateInitializationActivity](https://msdn2.microsoft.com/library/system.workflow.activities.stateinitializationactivity.aspx)|在进入某个状态时执行；可能包含其他活动。 有关详细信息，请参阅 [使用 StateInitialization 活动](https://msdn2.microsoft.com/library/bb675253.aspx)。|
|**StateFinalization**|[StateFinalizationActivity](https://msdn2.microsoft.com/library/system.workflow.activities.statefinalizationactivity.aspx)|离开 [StateActivity](https://msdn2.microsoft.com/library/system.workflow.activities.stateactivity.aspx) 活动时执行包含的活动。 有关详细信息，请参阅 [使用 StateFinalizationActivity 活动](https://msdn2.microsoft.com/library/bb675278.aspx)。|
|**EventDriven**|[EventDrivenActivity](https://msdn2.microsoft.com/library/system.workflow.activities.eventdrivenactivity.aspx)|用于依赖于外部事件开始执行的状态。 **EventDrivenActivity**活动必须有一个实现[IEventActivity](https://msdn2.microsoft.com/library/system.workflow.activities.ieventactivity.aspx)接口的活动，作为第一个子活动。 有关详细信息，请参阅 [使用 EventDrivenActivity 活动](https://msdn2.microsoft.com/library/bb628466.aspx)。|

 状态机工作流中的主要组件是 [StateActivity](https://msdn2.microsoft.com/library/system.workflow.activities.stateactivity.aspx) 活动。 在状态机工作流中的不同位置捕获了事件时，将会进入不同的状态，以处理与这些事件关联的任务。 在工作流的生存期内，工作流可能会离开和进入若干不同的状态。 这些状态通过使用 [SetStateActivity](https://msdn2.microsoft.com/library/system.workflow.activities.setstateactivity.aspx) 活动彼此连接。

 将新的 **StateActivity** 拖到工作流设计图面上时，可以将 [EventDrivenActivity](https://msdn2.microsoft.com/library/system.workflow.activities.eventdrivenactivity.aspx)、 [StateInitializationActivity](https://msdn2.microsoft.com/library/system.workflow.activities.stateinitializationactivity.aspx)、 [StateFinalizationActivity](https://msdn2.microsoft.com/library/system.workflow.activities.statefinalizationactivity.aspx)或其他 **StateActivity** 活动作为子活动添加。

> [!CAUTION]
> 使用状态机工作流设计器创建工作流时，必须使用 " **文档大纲** " 视图窗口监视正在设计的工作流的结构。 " **文档大纲** " 视图窗口中状态机工作流的结构视图反映了工作流标记文件中活动的逻辑布局。 工作流活动显示在设计图面上的物理布局可能不会反映工作流标记文件中活动的逻辑布局。
>
> 若要打开 " **文档大纲** " 窗口，请在 " **视图** " 菜单上，指向 " **其他窗口**"，然后选择 " **文档大纲**"。

## <a name="see-also"></a>另请参阅
 [如何：创建状态机工作流控制台应用程序 (旧) ](../workflow-designer/how-to-create-state-machine-workflow-console-applications-legacy.md)如何：使用[StateActivity 活动](https://msdn2.microsoft.com/library/bb628612.aspx) [Using the StateInitializationActivity Activity](https://msdn2.microsoft.com/library/bb675253.aspx) [创建状态机工作流库 (旧版) ](../workflow-designer/how-to-create-a-state-machine-workflow-library-legacy.md) [状态机工作流](https://msdn2.microsoft.com/library/bb628601.aspx)使用[StateFinalizationActivity 活动使用活动](https://msdn2.microsoft.com/library/bb675278.aspx)使用[SetStateActivity 活动](https://msdn2.microsoft.com/library/bb628469.aspx)使用[EventDrivenActivity](https://msdn2.microsoft.com/library/bb628466.aspx)活动
