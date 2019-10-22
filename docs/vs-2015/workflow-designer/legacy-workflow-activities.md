---
title: 旧版工作流活动 |Microsoft Docs
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
ms.openlocfilehash: f4f1110424aefc1771c0dc7600fb9996bff0e892
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658943"
---
# <a name="legacy-workflow-activities"></a>旧版工作流活动
[!INCLUDE[wf](../includes/wf-md.md)] 包含一组默认活动，这组活动提供了用于控制流、条件、事件处理、状态管理以及与应用程序和服务通信的功能。 在设计工作流时，可以使用 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 所提供的系统提供活动，也可以创建自己的自定义活动。

 下表列出了 [!INCLUDE[wf2](../includes/wf2-md.md)] 框架现成可用的活动集。 许多（但不是全部）活动都由可从 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 的 **"工具箱**" 访问的活动设计器表示。 若要创建活动，请从 "**工具箱**" 拖动其设计器，并将其放置到设计图面上。

|活动|描述|
|--------------|-----------------|
|[CallExternalMethodActivity](http://go.microsoft.com/fwlink?LinkID=65025)|与**HandleExternalEventActivity**活动结合使用，用于输入和输出与本地服务的通信。 [使用 CallExternalMethodActivity 活动](http://go.microsoft.com/fwlink?LinkID=65060)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[CancellationHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65050)|用于包含在所有复合活动的子项完成执行之前所取消复合活动的清理逻辑。 [使用 CancellationHandlerActivity 活动](http://go.microsoft.com/fwlink?LinkID=65061)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[CodeActivity](http://go.microsoft.com/fwlink?LinkID=65026)|使你能够向工作流中添加 Visual Basic 或 C# 代码。 [使用 CodeActivity 活动](http://go.microsoft.com/fwlink?LinkID=65062)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[CompensatableSequenceActivity](http://go.microsoft.com/fwlink?LinkID=65027)|[SequenceActivity](http://go.microsoft.com/fwlink?LinkID=65020)的可补偿版本。 [使用 CompensatableSequenceActivity 活动](http://go.microsoft.com/fwlink?LinkID=65002)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[CompensatableTransactionScopeActivity](http://go.microsoft.com/fwlink?LinkID=65051)|**TransactionScopeActivity**的可补偿版本。 [使用 CompensatableTransactionScopeActivity 活动](http://go.microsoft.com/fwlink?LinkID=65063)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[CompensateActivity](http://go.microsoft.com/fwlink?LinkID=65052)|使你能够调用代码来撤消或补偿发生错误时已由工作流执行的操作。 [使用 CompensateActivity 活动](http://go.microsoft.com/fwlink?LinkID=65064)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[CompensationHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65053)|一个或多个活动的包装，这些活动[使用 CompensationHandlerActivity 活动](http://go.microsoft.com/fwlink?LinkID=65065)[!INCLUDE[crdefault](../includes/crdefault-md.md)] 完成的 TransactionScopeActivity 活动的补偿。|
|[ConditionedActivityGroup](http://go.microsoft.com/fwlink?LinkID=65017)|基于适用于[ConditionedActivityGroup](http://go.microsoft.com/fwlink?LinkID=65017)活动本身的条件执行子活动，并基于单独应用于每个子项的条件执行子活动。 [使用 ConditionedActivityGroup 活动](http://go.microsoft.com/fwlink?LinkID=65066)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[DelayActivity](http://go.microsoft.com/fwlink?LinkID=65028)|使您能够在工作流中建立基于超时间隔的延迟。 [使用 DelayActivity 活动](http://go.microsoft.com/fwlink?LinkID=65067)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[EventDrivenActivity](http://go.microsoft.com/fwlink?LinkID=65029)|包装在指定事件发生时执行的一个或多个活动。 [使用 EventDrivenActivity 活动](http://go.microsoft.com/fwlink?LinkID=65068)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[EventHandlersActivity](http://go.microsoft.com/fwlink?LinkID=65018)|提供一个用于将事件与活动关联的框架。 [使用 EventHandlersActivity 活动](http://go.microsoft.com/fwlink?LinkID=65069)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[EventHandlingScopeActivity](http://go.microsoft.com/fwlink?LinkID=65030)|同时执行其[EventHandlersActivity](http://go.microsoft.com/fwlink?LinkID=65018)的子活动。 [使用 EventHandlingScopeActivity 活动](http://go.microsoft.com/fwlink?LinkID=65070)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[FaultHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65054)|用于处理指定类型的异常。 [使用 FaultHandlerActivity 活动](http://go.microsoft.com/fwlink?LinkID=65071)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[FaultHandlersActivity](http://go.microsoft.com/fwlink?LinkID=65055)|表示一个复合活动，它具有一个类型为[FaultHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65054)的子活动的有序列表。 [使用 FaultHandlersActivity 活动](http://go.microsoft.com/fwlink?LinkID=65072)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[HandleExternalEventActivity](http://go.microsoft.com/fwlink?LinkID=65031)|与[CallExternalMethodActivity](http://go.microsoft.com/fwlink?LinkID=65025)活动结合使用，用于输入和输出与本地服务的通信。 [使用 HandleExternalEventActivity 活动](http://go.microsoft.com/fwlink?LinkID=65073)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[IfElseActivity](http://go.microsoft.com/fwlink?LinkID=65033)|测试每个分支上的条件，并在条件等于**true**的第一个分支上执行活动。 [使用 IfElseActivity 活动](http://go.microsoft.com/fwlink?LinkID=65074)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[IfElseBranchActivity](http://go.microsoft.com/fwlink?LinkID=65034)|表示[IfElseActivity](http://go.microsoft.com/fwlink?LinkID=65033)的分支。 [使用 IfElseBranchActivity 活动](http://go.microsoft.com/fwlink?LinkID=65075)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[InvokeWebServiceActivity](http://go.microsoft.com/fwlink?LinkID=65035)|使工作流能够调用 Web 服务。 [使用 InvokeWebServiceActivity 活动](http://go.microsoft.com/fwlink?LinkID=65076)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[InvokeWorkflowActivity](http://go.microsoft.com/fwlink?LinkID=65036)|使工作流能够调用其他工作流。 [使用 InvokeWorkflowActivity 活动](http://go.microsoft.com/fwlink?LinkID=65077)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[ListenActivity](http://go.microsoft.com/fwlink?LinkID=65037)|只包含[EventDrivenActivity](http://go.microsoft.com/fwlink?LinkID=65029)子活动的复合活动。 [使用 ListenActivity 活动](http://go.microsoft.com/fwlink?LinkID=65078)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[ParallelActivity](http://go.microsoft.com/fwlink?LinkID=65038)|提供一种方法，用于计划同时处理两个或更多个子**SequenceActivity**活动分支。 [使用 ParallelActivity 活动](http://go.microsoft.com/fwlink?LinkID=65079)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65019)|用于表示规则的集合。 规则由条件和引起的操作组成。 [使用 PolicyActivity 活动](http://go.microsoft.com/fwlink?LinkID=65004)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[ReplicatorActivity](http://go.microsoft.com/fwlink?LinkID=65039)|创建单个子活动的多个实例。 [使用 ReplicatorActivity 活动](http://go.microsoft.com/fwlink?LinkID=65080)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[SequenceActivity](http://go.microsoft.com/fwlink?LinkID=65020)|提供了一种简单的方法，可将多个活动链接在一起以按顺序执行。 [使用 SequenceActivity 活动](http://go.microsoft.com/fwlink?LinkID=65081)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[SetStateActivity](http://go.microsoft.com/fwlink?LinkID=65041)|指定到新状态的转换。 [使用 SetStateActivity 活动](http://go.microsoft.com/fwlink?LinkID=65082)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[StateActivity](http://go.microsoft.com/fwlink?LinkID=65042)|表示状态机工作流中的一个状态。 [使用 StateActivity 活动](http://go.microsoft.com/fwlink?LinkID=65083)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[StateFinalizationActivity](http://go.microsoft.com/fwlink?LinkID=65043)|在[StateActivity](http://go.microsoft.com/fwlink?LinkID=65042)活动中用作子活动的容器，这些子活动是在离开**StateActivity**活动时执行的。 [使用 StateFinalizationActivity 活动](http://go.microsoft.com/fwlink?LinkID=65008)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[StateInitializationActivity](http://go.microsoft.com/fwlink?LinkID=65044)|在[StateActivity](http://go.microsoft.com/fwlink?LinkID=65042)活动中用作子活动的容器，这些子活动是在进入**StateActivity**活动时执行的。 [使用 StateInitializationActivity 活动](http://go.microsoft.com/fwlink?LinkID=65006)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[SuspendActivity](http://go.microsoft.com/fwlink?LinkID=65056)|挂起工作流的操作，以便能够在出现某种需要特别注意的错误情况时进行干预。 [使用 SuspendActivity 活动](http://go.microsoft.com/fwlink?LinkID=65084)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[SynchronizationScopeActivity](http://go.microsoft.com/fwlink?LinkID=65057)|在同步的域中按顺序执行所包含的活动。 [使用 SynchronizationScopeActivity 活动](http://go.microsoft.com/fwlink?LinkID=65085)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[TerminateActivity](http://go.microsoft.com/fwlink?LinkID=65058)|使您能够在发生错误情形时立即结束工作流的操作。 [使用 TerminateActivity 活动](http://go.microsoft.com/fwlink?LinkID=65086)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[ThrowActivity](http://go.microsoft.com/fwlink?LinkID=65059)|使您能够捕获作为工作流过程元数据一部分引发的业务异常。 [使用 ThrowActivity 活动](http://go.microsoft.com/fwlink?LinkID=65087)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[TransactionScopeActivity](http://go.microsoft.com/fwlink?LinkID=65093)|提供一个用于事务和异常处理的框架。 有关详细信息，请参阅[使用 TransactionScopeActivity 活动](http://go.microsoft.com/fwlink?LinkID=65088)。|
|[WebServiceFaultActivity](http://go.microsoft.com/fwlink?LinkID=65046)|使你能够建立所出现 Web 服务错误的模型。 [使用 WebServiceFaultActivity 活动](http://go.microsoft.com/fwlink?LinkID=65089)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[WebServiceInputActivity](http://go.microsoft.com/fwlink?LinkID=65047)|接收来自 Web 服务的数据。 [使用 WebServiceInputActivity 活动](http://go.microsoft.com/fwlink?LinkID=65090)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[WebServiceOutputActivity](http://go.microsoft.com/fwlink?LinkID=65048)|对工作流发出的 Web 服务请求做出响应。 [使用 WebServiceOutputActivity 活动](http://go.microsoft.com/fwlink?LinkID=65092)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|
|[WhileActivity](http://go.microsoft.com/fwlink?LinkID=65049)|使工作流能够在条件得到满足之前进行循环。 [使用 WhileActivity 活动](http://go.microsoft.com/fwlink?LinkID=65091)[!INCLUDE[crdefault](../includes/crdefault-md.md)]。|

 [!INCLUDE[crabout](../includes/crabout-md.md)] 如何创建自定义活动，请参阅[开发自定义活动](http://go.microsoft.com/fwlink?LinkID=65023)和[使用旧版活动设计器](../workflow-designer/using-the-legacy-activity-designer.md)。

## <a name="in-this-section"></a>本节内容
 [活动视图（旧版）](../workflow-designer/activity-views-legacy.md)介绍活动的不同设计视图。

 [如何：向工具箱添加活动（旧版）](../workflow-designer/how-to-add-activities-to-the-toolbox-legacy.md)演示如何将活动添加到 "工具箱"。

 [如何：创建声明性规则条件（旧版）](../workflow-designer/how-to-create-a-declarative-rule-condition-legacy.md)显示创建声明性规则条件的步骤。

 [如何：创建 PolicyActivity 规则集（旧版）](../workflow-designer/how-to-create-a-policyactivity-rule-set-legacy.md)显示创建 PolicyActivity 规则集的步骤。

 [如何：实现 WCF 协定操作（旧版）](../workflow-designer/how-to-implement-a-windows-communication-foundation-contract-operation-legacy.md)演示实现 [!INCLUDE[indigo2](../includes/indigo2-md.md)] 合同操作的步骤。

 [如何：调用 WCF 协定操作（旧版）](../workflow-designer/how-to-invoke-a-windows-communication-foundation-contract-operation-legacy.md)显示调用 [!INCLUDE[indigo2](../includes/indigo2-md.md)] 合同操作的步骤。

## <a name="see-also"></a>请参阅
 [Windows Workflow Foundation 活动](http://go.microsoft.com/fwlink?LinkID=65005)[开发](http://go.microsoft.com/fwlink?LinkID=65010)[工作流开发工作流活动](http://go.microsoft.com/fwlink?LinkID=65023)