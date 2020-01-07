---
title: 工作流设计器并行活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Parallel.UI
ms.assetid: 0306dc3b-075a-4091-ac3a-96486fbabed5
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3f07dd02f682cd5c61d4d17099c1aeb76bb39bf8
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593156"
---
# <a name="parallel-activity-designer"></a>Parallel 活动设计器

<xref:System.Activities.Statements.Parallel> 活动并发执行一组子活动。

## <a name="the-parallel-activity"></a>Parallel 活动

<xref:System.Activities.Statements.Parallel> 活动将其子活动存储在 <xref:System.Activities.Statements.Parallel.Branches%2A> 集合中。 如果某些子活动可能进入空闲状态，则使用 <xref:System.Activities.Statements.Parallel> 活动，而不使用 <xref:System.Activities.Statements.Sequence> 活动。

<xref:System.Activities.Statements.Parallel> 活动具有一个 <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> 属性，该属性包含一个指定 Visual Basic 表达式的用户。 <xref:System.Activities.Statements.Parallel> 活动在完成每个分支后计算此属性。 如果计算结果为**True**，则 <xref:System.Activities.Statements.Parallel> 活动完成，而不执行其他分支。 如果 <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> 的计算结果不为**True**，则在完成其所有子活动后 <xref:System.Activities.Statements.Parallel> 活动完成。

### <a name="using-the-parallel-activity-designer"></a>使用 Parallel 活动设计器

访问 "**工具箱**" 的 "**控制流**" 类别中的 "**并行**活动设计器"。

可以将 "**并行**" 活动设计器从 "**工具箱**" 拖放到工作流设计器图面上通常放置活动设计器的任何位置，例如，在 " **Sequence** " 活动设计器内。 将其放入工作流设计器后，它将创建一个 <xref:System.Activities.Statements.Parallel> 活动，该活动默认包含**并行**的 <xref:System.Activities.Activity.DisplayName%2A>

若要向并行活动的 <xref:System.Activities.Statements.Parallel.Branches%2A> 集合中添加活动，请将其他活动设计器从 "**工具箱**" 拖放到 "**并行**" 活动设计器内的三角形上。 三角形位于分支中包含的活动的侧面。 可通过重复此过程过来添加其他活动。 可以通过将活动拖放到 "**并行**" 活动设计器中对其进行重新排序。

### <a name="parallel-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 Parallel 活动属性

下表列出 Parallel 活动属性并说明如何在设计器中使用这些属性。

|属性名|必需|用量|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定活动设计器在标头中的友好显示名称。 默认值为 "**并行**"。 可以在 "**属性**" 网格中或直接在活动设计器标头中编辑该值。|
|<xref:System.Activities.Statements.Parallel.Branches%2A>|True|包含要执行的子活动的集合。|
|<xref:System.Activities.Statements.Parallel.CompletionCondition%2A>|False|在分支完成后计算。 如果计算结果为**True**，则取消计划的挂起分支。 如果未将此属性设置为或计算为**False**，则在完成其所有子活动后，活动完成。 默认值为 **null**。|

## <a name="see-also"></a>另请参阅

- [Sequence](../workflow-designer/sequence-activity-designer.md)
- [ParallelForEach\<T>](../workflow-designer/parallelforeach-t-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)
