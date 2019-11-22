---
title: Legacy Workflow Activities | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- workflows, activities
- activities
- workflow activities
ms.assetid: 4af7a06b-1e82-43c8-aec8-0dc5fb63d08a
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e6bdfb5e2a51a274bd5f0490954a2825a2e488c5
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302950"
---
# <a name="legacy-workflow-activities"></a>旧版工作流活动
[!INCLUDE[wf](../includes/wf-md.md)] 包含一组默认活动，这组活动提供了用于控制流、条件、事件处理、状态管理以及与应用程序和服务通信的功能。 在设计工作流时，可以使用 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 所提供的系统提供活动，也可以创建自己的自定义活动。

 下表列出了 [!INCLUDE[wf2](../includes/wf2-md.md)] 框架现成可用的活动集。 Many, but not all, of these activities are represented by activity designers that can be accessed from the **Toolbox** of the [!INCLUDE[wfd2](../includes/wfd2-md.md)]. To create an activity, drag its designer from the **Toolbox** and drop it on the design surface.

|活动|描述|
|--------------|-----------------|
|[CallExternalMethodActivity](https://go.microsoft.com/fwlink?LinkID=65025)|Used with the **HandleExternalEventActivity** activity for input and output communications with a local service. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the CallExternalMethodActivity Activity](https://go.microsoft.com/fwlink?LinkID=65060).|
|[CancellationHandlerActivity](https://go.microsoft.com/fwlink?LinkID=65050)|用于包含在所有复合活动的子项完成执行之前所取消复合活动的清理逻辑。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the CancellationHandlerActivity Activity](https://go.microsoft.com/fwlink?LinkID=65061).|
|[CodeActivity](https://go.microsoft.com/fwlink?LinkID=65026)|使你能够向工作流中添加 Visual Basic 或 C# 代码。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the CodeActivity Activity](https://go.microsoft.com/fwlink?LinkID=65062).|
|[CompensatableSequenceActivity](https://go.microsoft.com/fwlink?LinkID=65027)|A compensatable version of [SequenceActivity](https://go.microsoft.com/fwlink?LinkID=65020). [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the CompensatableSequenceActivity Activity](https://go.microsoft.com/fwlink?LinkID=65002).|
|[CompensatableTransactionScopeActivity](https://go.microsoft.com/fwlink?LinkID=65051)|A compensatable version of **TransactionScopeActivity**. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the CompensatableTransactionScopeActivity Activity](https://go.microsoft.com/fwlink?LinkID=65063).|
|[CompensateActivity](https://go.microsoft.com/fwlink?LinkID=65052)|使你能够调用代码来撤消或补偿发生错误时已由工作流执行的操作。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the CompensateActivity Activity](https://go.microsoft.com/fwlink?LinkID=65064).|
|[CompensationHandlerActivity](https://go.microsoft.com/fwlink?LinkID=65053)|A wrapper for one or more activities that perform compensation for a completed TransactionScopeActivity activity [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the CompensationHandlerActivity Activity](https://go.microsoft.com/fwlink?LinkID=65065).|
|[ConditionedActivityGroup](https://go.microsoft.com/fwlink?LinkID=65017)|Executes child activities based on a condition that applies to the [ConditionedActivityGroup](https://go.microsoft.com/fwlink?LinkID=65017) activity itself and based on conditions that apply separately to each child. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the ConditionedActivityGroup Activity](https://go.microsoft.com/fwlink?LinkID=65066).|
|[DelayActivity](https://go.microsoft.com/fwlink?LinkID=65028)|使您能够在工作流中建立基于超时间隔的延迟。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the DelayActivity Activity](https://go.microsoft.com/fwlink?LinkID=65067).|
|[EventDrivenActivity](https://go.microsoft.com/fwlink?LinkID=65029)|包装在指定事件发生时执行的一个或多个活动。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the EventDrivenActivity Activity](https://go.microsoft.com/fwlink?LinkID=65068).|
|[EventHandlersActivity](https://go.microsoft.com/fwlink?LinkID=65018)|提供一个用于将事件与活动关联的框架。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the EventHandlersActivity Activity](https://go.microsoft.com/fwlink?LinkID=65069).|
|[EventHandlingScopeActivity](https://go.microsoft.com/fwlink?LinkID=65030)|Executes its main child activity concurrently with an [EventHandlersActivity](https://go.microsoft.com/fwlink?LinkID=65018). [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the EventHandlingScopeActivity Activity](https://go.microsoft.com/fwlink?LinkID=65070).|
|[FaultHandlerActivity](https://go.microsoft.com/fwlink?LinkID=65054)|用于处理指定类型的异常。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the FaultHandlerActivity Activity](https://go.microsoft.com/fwlink?LinkID=65071).|
|[FaultHandlersActivity](https://go.microsoft.com/fwlink?LinkID=65055)|Represents a composite activity that has an ordered list of child activities of type [FaultHandlerActivity](https://go.microsoft.com/fwlink?LinkID=65054). [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the FaultHandlersActivity Activity](https://go.microsoft.com/fwlink?LinkID=65072).|
|[HandleExternalEventActivity](https://go.microsoft.com/fwlink?LinkID=65031)|Used in conjunction with the [CallExternalMethodActivity](https://go.microsoft.com/fwlink?LinkID=65025) activity for input and output communications with a local service. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the HandleExternalEventActivity Activity](https://go.microsoft.com/fwlink?LinkID=65073).|
|[IfElseActivity](https://go.microsoft.com/fwlink?LinkID=65033)|Tests a condition on each branch and performs activities on the first branch for which the condition equals **true**. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the IfElseActivity Activity](https://go.microsoft.com/fwlink?LinkID=65074).|
|[IfElseBranchActivity](https://go.microsoft.com/fwlink?LinkID=65034)|Represents a branch of an [IfElseActivity](https://go.microsoft.com/fwlink?LinkID=65033). [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the IfElseBranchActivity Activity](https://go.microsoft.com/fwlink?LinkID=65075).|
|[InvokeWebServiceActivity](https://go.microsoft.com/fwlink?LinkID=65035)|使工作流能够调用 Web 服务。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the InvokeWebServiceActivity Activity](https://go.microsoft.com/fwlink?LinkID=65076).|
|[InvokeWorkflowActivity](https://go.microsoft.com/fwlink?LinkID=65036)|使工作流能够调用其他工作流。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the InvokeWorkflowActivity Activity](https://go.microsoft.com/fwlink?LinkID=65077).|
|[ListenActivity](https://go.microsoft.com/fwlink?LinkID=65037)|A composite activity that contains only [EventDrivenActivity](https://go.microsoft.com/fwlink?LinkID=65029) child activities. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the ListenActivity Activity](https://go.microsoft.com/fwlink?LinkID=65078).|
|[ParallelActivity](https://go.microsoft.com/fwlink?LinkID=65038)|Provides a way to schedule two or more child **SequenceActivity** activity branches for processing at the same time. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the ParallelActivity Activity](https://go.microsoft.com/fwlink?LinkID=65079).|
|[PolicyActivity](https://go.microsoft.com/fwlink?LinkID=65019)|用于表示规则的集合。 规则由条件和引起的操作组成。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the PolicyActivity Activity](https://go.microsoft.com/fwlink?LinkID=65004).|
|[ReplicatorActivity](https://go.microsoft.com/fwlink?LinkID=65039)|创建单个子活动的多个实例。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the ReplicatorActivity Activity](https://go.microsoft.com/fwlink?LinkID=65080).|
|[SequenceActivity](https://go.microsoft.com/fwlink?LinkID=65020)|提供了一种简单的方法，可将多个活动链接在一起以按顺序执行。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the SequenceActivity Activity](https://go.microsoft.com/fwlink?LinkID=65081).|
|[SetStateActivity](https://go.microsoft.com/fwlink?LinkID=65041)|指定到新状态的转换。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the SetStateActivity Activity](https://go.microsoft.com/fwlink?LinkID=65082).|
|[StateActivity](https://go.microsoft.com/fwlink?LinkID=65042)|表示状态机工作流中的一个状态。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the StateActivity Activity](https://go.microsoft.com/fwlink?LinkID=65083).|
|[StateFinalizationActivity](https://go.microsoft.com/fwlink?LinkID=65043)|Used in a [StateActivity](https://go.microsoft.com/fwlink?LinkID=65042) activity as a container for child activities that are executed when leaving the **StateActivity** activity. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the StateFinalizationActivity Activity](https://go.microsoft.com/fwlink?LinkID=65008).|
|[StateInitializationActivity](https://go.microsoft.com/fwlink?LinkID=65044)|Used in a [StateActivity](https://go.microsoft.com/fwlink?LinkID=65042) activity as a container for child activities that are executed when entering the **StateActivity** activity. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the StateInitializationActivity Activity](https://go.microsoft.com/fwlink?LinkID=65006).|
|[SuspendActivity](https://go.microsoft.com/fwlink?LinkID=65056)|挂起工作流的操作，以便能够在出现某种需要特别注意的错误情况时进行干预。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the SuspendActivity Activity](https://go.microsoft.com/fwlink?LinkID=65084).|
|[SynchronizationScopeActivity](https://go.microsoft.com/fwlink?LinkID=65057)|在同步的域中按顺序执行所包含的活动。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the SynchronizationScopeActivity Activity](https://go.microsoft.com/fwlink?LinkID=65085).|
|[TerminateActivity](https://go.microsoft.com/fwlink?LinkID=65058)|使您能够在发生错误情形时立即结束工作流的操作。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the TerminateActivity Activity](https://go.microsoft.com/fwlink?LinkID=65086).|
|[ThrowActivity](https://go.microsoft.com/fwlink?LinkID=65059)|使您能够捕获作为工作流过程元数据一部分引发的业务异常。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the ThrowActivity Activity](https://go.microsoft.com/fwlink?LinkID=65087).|
|[TransactionScopeActivity](https://go.microsoft.com/fwlink?LinkID=65093)|提供一个用于事务和异常处理的框架。 For more information, see [Using the TransactionScopeActivity Activity](https://go.microsoft.com/fwlink?LinkID=65088).|
|[WebServiceFaultActivity](https://go.microsoft.com/fwlink?LinkID=65046)|使你能够建立所出现 Web 服务错误的模型。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the WebServiceFaultActivity Activity](https://go.microsoft.com/fwlink?LinkID=65089).|
|[WebServiceInputActivity](https://go.microsoft.com/fwlink?LinkID=65047)|接收来自 Web 服务的数据。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the WebServiceInputActivity Activity](https://go.microsoft.com/fwlink?LinkID=65090).|
|[WebServiceOutputActivity](https://go.microsoft.com/fwlink?LinkID=65048)|对工作流发出的 Web 服务请求做出响应。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the WebServiceOutputActivity Activity](https://go.microsoft.com/fwlink?LinkID=65092).|
|[WhileActivity](https://go.microsoft.com/fwlink?LinkID=65049)|使工作流能够在条件得到满足之前进行循环。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][Using the WhileActivity Activity](https://go.microsoft.com/fwlink?LinkID=65091).|

 [!INCLUDE[crabout](../includes/crabout-md.md)] how to create custom activities, see [Developing Custom Activities](https://go.microsoft.com/fwlink?LinkID=65023) and [Using the Legacy Activity Designer](../workflow-designer/using-the-legacy-activity-designer.md).

## <a name="in-this-section"></a>本节内容
 [Activity Views (Legacy)](../workflow-designer/activity-views-legacy.md) Describes the different design views of activities.

 [How to: Add Activities to the Toolbox (Legacy)](../workflow-designer/how-to-add-activities-to-the-toolbox-legacy.md) Shows how to add activities to the toolbox.

 [How to: Create a Declarative Rule Condition (Legacy)](../workflow-designer/how-to-create-a-declarative-rule-condition-legacy.md) Shows the steps to create a declarative rule condition.

 [How to: Create a PolicyActivity Rule Set (Legacy)](../workflow-designer/how-to-create-a-policyactivity-rule-set-legacy.md) Shows the steps to create a PolicyActivity rule set.

 [How to: Implement a WCF Contract Operation (Legacy)](../workflow-designer/how-to-implement-a-windows-communication-foundation-contract-operation-legacy.md) Shows the steps to implement a [!INCLUDE[indigo2](../includes/indigo2-md.md)] contract operation.

 [How to: Invoke a WCF Contract Operation (Legacy)](../workflow-designer/how-to-invoke-a-windows-communication-foundation-contract-operation-legacy.md) Shows the steps to invoke a [!INCLUDE[indigo2](../includes/indigo2-md.md)] contract operation.

## <a name="see-also"></a>请参阅
 [Windows Workflow Foundation Activities](https://go.microsoft.com/fwlink?LinkID=65005) [Developing Workflows](https://go.microsoft.com/fwlink?LinkID=65010) [Developing Workflow Activities](https://go.microsoft.com/fwlink?LinkID=65023)