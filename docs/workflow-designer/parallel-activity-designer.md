---
title: 工作流设计器-Parallel 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Parallel.UI
ms.assetid: 0306dc3b-075a-4091-ac3a-96486fbabed5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 79e1e7e48f7ed7e8cd4084805dfae2018a886a82
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63002776"
---
# <a name="parallel-activity-designer"></a>Parallel 活动设计器

<xref:System.Activities.Statements.Parallel> 活动并发执行一组子活动。

## <a name="the-parallel-activity"></a>Parallel 活动

<xref:System.Activities.Statements.Parallel> 活动将其子活动存储在 <xref:System.Activities.Statements.Parallel.Branches%2A> 集合中。 如果某些子活动可能进入空闲状态，则使用 <xref:System.Activities.Statements.Parallel> 活动，而不使用 <xref:System.Activities.Statements.Sequence> 活动。

<xref:System.Activities.Statements.Parallel>活动具有<xref:System.Activities.Statements.Parallel.CompletionCondition%2A>属性，其中包含用户指定 Visual Basic 表达式。 <xref:System.Activities.Statements.Parallel> 活动在完成每个分支后计算此属性。 如果其计算结果为 **，则返回 True**，则<xref:System.Activities.Statements.Parallel>活动完成而无需执行其他分支。 如果<xref:System.Activities.Statements.Parallel.CompletionCondition%2A>的计算结果不**True**，然后<xref:System.Activities.Statements.Parallel>活动完成其所有子活动后完成。

### <a name="using-the-parallel-activity-designer"></a>使用 Parallel 活动设计器

访问**并行**中的活动设计器**控制流**类别**工具箱**。

**并行**活动设计器可以从拖动**工具箱**和放置到工作流设计器图面，无论在何处放置活动设计器是通常情况下，例如，内部**序列**活动设计器。 之后将它放到工作流设计器，它会创建<xref:System.Activities.Statements.Parallel>活动，其中默认情况下包含<xref:System.Activities.Activity.DisplayName%2A>的**并行**

若要向其中添加活动<xref:System.Activities.Statements.Parallel.Branches%2A>并行活动的集合将一些其他活动设计器从**工具箱**拖放到内的三角形**并行**活动设计器。 三角形位于分支中包含的活动的侧面。 可通过重复此过程过来添加其他活动。 活动可以通过拖放在重新排序**并行**活动设计器。

### <a name="parallel-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 Parallel 活动属性

下表列出 Parallel 活动属性并说明如何在设计器中使用这些属性。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定活动设计器在标头中的友好显示名称。 默认值是**并行**。 值可以根据需要在中编辑**属性**网格或直接在活动设计器标头。|
|<xref:System.Activities.Statements.Parallel.Branches%2A>|True|包含要执行的子活动的集合。|
|<xref:System.Activities.Statements.Parallel.CompletionCondition%2A>|False|在分支完成后计算。 如果其计算结果为 **，则返回 True**，然后计划取消挂起的分支。 如果此属性未设置或计算结果为**False**，活动完成其所有子活动后完成。 默认值是**null**。|

## <a name="see-also"></a>请参阅

- [Sequence](../workflow-designer/sequence-activity-designer.md)
- [ParallelForEach\<T>](../workflow-designer/parallelforeach-t-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)