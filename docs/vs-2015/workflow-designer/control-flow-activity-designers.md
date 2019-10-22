---
title: 控制流活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: ba74af23-5398-4e62-bd90-c50612e3bfef
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 40f17913864f80e04c3e8b8e703f057094c9bdea
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656929"
---
# <a name="control-flow-activity-designers"></a>控制流活动设计器
[!INCLUDE[wfd1](../includes/wfd1-md.md)] 包含系统提供的若干活动，构造工作流时可以使用它们。 本节包含系统提供的活动中用于控制工作流中的流的活动。 以下主题介绍这些活动以及如何使用它们。

## <a name="in-this-section"></a>本节内容
 [DoWhile](../workflow-designer/dowhile-activity-designer.md)执行其主体中包含的活动至少一次，直到指定条件的计算结果为**true**。

 [ForEach \<T >](foreach-t-activity-designer.md)对指定集合中的每个项执行其主体中包含的活动。

 [如果](../workflow-designer/if-activity-designer.md)计算条件并根据该计算结果执行活动。

 [并行](../workflow-designer/parallel-activity-designer.md)并发执行子活动的集合。

 [ParallelForEach \<T >](../workflow-designer/parallelforeach-t-activity-designer.md)枚举集合中的元素，并对集合中的每个元素并行执行嵌入语句

 [选取](../workflow-designer/pick-activity-designer.md)执行多个分支中的一个，以响应提供基于事件的流控制的某个事件。

 [PickBranch](../workflow-designer/pickbranch-activity-designer.md)在 <xref:System.Activities.Statements.Pick> 活动中提供可能的执行路径。

 [序列](../workflow-designer/sequence-activity-designer.md)包含按顺序执行的子活动的有序集合。

 [切换 \<T >](switch-t-activity-designer.md)计算指定的表达式，并执行活动集合中的活动，这些活动的关联键与从计算中获取的值匹配。

 [While](../workflow-designer/while-activity-designer.md)在指定条件的计算结果为**true**的情况下执行其主体中包含的活动。

## <a name="reference"></a>参考
 <xref:System.Activities.Activity>

 <xref:System.Activities.Statements.DoWhile>

 <xref:System.Activities.Statements.ForEach%601>

 <xref:System.Activities.Statements.If>

 <xref:System.Activities.Statements.Parallel>

 <xref:System.Activities.Statements.ParallelForEach%601>

 <xref:System.Activities.Statements.Pick>

 <xref:System.Activities.Statements.PickBranch>

 <xref:System.Activities.Statements.Sequence>

 <xref:System.Activities.Statements.Switch%601>

 <xref:System.Activities.Statements.While>

## <a name="related-sections"></a>相关章节
 有关其他类型活动设计器的信息，请参见下列主题。

 [使用活动设计器](../workflow-designer/using-the-activity-designers.md)

 [流程图](../workflow-designer/flowchart-activity-designers.md)

 [Messaging](../workflow-designer/messaging-activity-designers.md)

 [运行时](../workflow-designer/runtime-activity-designers.md)

 [基元](../workflow-designer/primitives-activity-designers.md)

 [事务](../workflow-designer/transaction-activity-designers.md)

 [收集](../workflow-designer/collection-activity-designers.md)

 [错误处理](../workflow-designer/error-handling-activity-designers.md)

## <a name="external-resources"></a>外部资源
 [使用活动设计器](../workflow-designer/using-the-activity-designers.md)