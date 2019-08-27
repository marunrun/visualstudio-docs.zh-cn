---
title: 并行活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Parallel.UI
ms.assetid: 0306dc3b-075a-4091-ac3a-96486fbabed5
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 627a99fec632871b815904abd798c0e4bbfd6505
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62971337"
---
# <a name="parallel-activity-designer"></a>Parallel 活动设计器
<xref:System.Activities.Statements.Parallel> 活动并发执行一组子活动。  
  
## <a name="the-parallel-activity"></a>Parallel 活动  
 <xref:System.Activities.Statements.Parallel> 活动将其子活动存储在 <xref:System.Activities.Statements.Parallel.Branches%2A> 集合中。 如果某些子活动可能进入空闲状态，则使用 <xref:System.Activities.Statements.Parallel> 活动，而不使用 <xref:System.Activities.Statements.Sequence> 活动。  
  
 <xref:System.Activities.Statements.Parallel> 活动有一个 <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> 属性，该属性包含用户指定的 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 表达式。 <xref:System.Activities.Statements.Parallel> 活动在完成每个分支后计算此属性。 如果其计算结果为 **，则返回 True**，则<xref:System.Activities.Statements.Parallel>活动完成而无需执行其他分支。 如果<xref:System.Activities.Statements.Parallel.CompletionCondition%2A>的计算结果不**True**，然后<xref:System.Activities.Statements.Parallel>活动完成其所有子活动后完成。  
  
### <a name="using-the-parallel-activity-designer"></a>使用 Parallel 活动设计器  
 **并行**活动设计器可在**控制流**类别**工具箱**，这通过单击来访问**工具箱**选项卡上的左侧和右侧[!INCLUDE[wfd2](../includes/wfd2-md.md)](或者，选择**工具栏**从**视图**菜单或 CTRL + ALT + X。)  
  
 **并行**活动设计器可以从拖动**工具箱**拖放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面上活动设计器放置的任何位置通常情况下，例如，内部**序列**活动设计器。 之后设计器放入[!INCLUDE[wfd2](../includes/wfd2-md.md)]，它将创建<xref:System.Activities.Statements.Parallel>活动，其中默认情况下包含<xref:System.Activities.Activity.DisplayName%2A>的**并行**  
  
 若要向其中添加活动<xref:System.Activities.Statements.Parallel.Branches%2A>并行活动的集合将一些其他活动设计器从**工具箱**拖放到内的三角形**并行**活动设计器。 三角形位于分支中包含的活动的侧面。 可通过重复此过程过来添加其他活动。 活动可以通过拖放在重新排序**并行**活动设计器。  
  
### <a name="parallel-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 Parallel 活动属性  
 下表列出 Parallel 活动属性并说明如何在设计器中使用这些属性。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定活动设计器在标头中的友好显示名称。 默认值是**并行**。 值可以根据需要在中编辑**属性**网格或直接在活动设计器标头。|  
|<xref:System.Activities.Statements.Parallel.Branches%2A>|True|包含要执行的子活动的集合。|  
|<xref:System.Activities.Statements.Parallel.CompletionCondition%2A>|False|在分支完成后计算。 如果其计算结果为 **，则返回 True**，然后计划取消挂起的分支。 如果此属性未设置或计算结果为**False**，活动完成其所有子活动后完成。 默认值是**null**。|  
  
## <a name="see-also"></a>请参阅  
 [序列](../workflow-designer/sequence-activity-designer.md)   
 [ParallelForEach\<T>](../workflow-designer/parallelforeach-t-activity-designer.md)   
 [控制流](../workflow-designer/control-flow-activity-designers.md)