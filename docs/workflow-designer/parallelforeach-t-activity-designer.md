---
title: ParallelForEach &lt; T &gt; 活动设计器工作流设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ParallelForEach`1.UI
ms.assetid: e93a4843-aef2-4d3e-9a0a-a2d3d1411aa7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8e2d3d33b150bd9c360896f88eddf032837fe9c9
ms.sourcegitcommit: 186c0c250d85ac74274fa1e438b4c7c7108d8a36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86876042"
---
# <a name="parallelforeach-activity-designer"></a>ParallelForEach 活动设计器

<xref:System.Activities.Statements.ParallelForEach%601> 活动枚举集合元素并对集合中的每个元素并行执行嵌入语句，这将在同一线程上异步执行。 如果此活动的子活动预期会进入空闲状态，请使用此流控制活动，而不是 <xref:System.Activities.Statements.Sequence> 活动。

<xref:System.Activities.Statements.ParallelForEach%601>活动具有一个 <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> 属性，该属性包含 Visual Basic 表达式指定的用户。 <xref:System.Activities.Statements.ParallelForEach%601> 活动在完成每个分支后计算此属性。 如果计算结果为**true**，则 <xref:System.Activities.Statements.ParallelForEach%601> 活动完成，而不执行其他分支。 如果 <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> 计算结果不为**true**，则在 <xref:System.Activities.Statements.ParallelForEach%601> 完成其所有子活动后，活动完成。

## <a name="the-parallelforeacht-activity"></a>ParallelForEach<T \> 活动

<xref:System.Activities.Statements.ParallelForEach%601>枚举其值并 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 为其所枚举的每个值计划。 仅安排 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 的执行顺序。 Body 的执行方式取决于 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 是否进入空闲状态。

如果 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 未进入空闲状态，则会按相反顺序执行，因为安排的活动作为堆栈来处理，最后安排的活动最先执行。 例如，如果在中有一个集合 {1,2,3,4} <xref:System.Activities.Statements.ParallelForEach%601> ，并使用**WriteLine**作为正文来写入值。已在控制台中打印4、3、2、1。 这是因为， **WriteLine**不会处于空闲状态，因此在计划4个**writeline**活动后，将使用堆栈行为（在最后一个结束时）执行该操作。

但是如果 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 中有会进入空闲状态的活动，如 <xref:System.ServiceModel.Activities.Receive> 活动或 <xref:System.Activities.Statements.Delay> 活动， 那么就不需要等待它们完成。 <xref:System.Activities.Statements.ParallelForEach%601> 转至下一个预定的主体活动，并尝试执行它。 如果该活动也进入空闲状态，则 <xref:System.Activities.Statements.ParallelForEach%601> 将再移到下一个 Body 活动。

### <a name="using-the-parallelforeacht-activity-designer"></a>使用 ParallelForEach \<T> 活动设计器

访问 "**工具箱**" 的 "**控制流**" 类别中的 " **ParallelForEach \<T> ** " 活动设计器。

可以将 " ** \<T> ParallelForEach** " 活动设计器从 "**工具箱**" 拖放到工作流设计器图面上通常放置活动设计器的任何位置，例如，在 " **Sequence** " 活动设计器内。 将其放入工作流设计器后，它将创建一个 <xref:System.Activities.Statements.ParallelForEach%601> 活动，该活动默认包含 <xref:System.Activities.Activity.DisplayName%2A> **ParallelForEach<Int32 的 \> 。**

### <a name="parallelforeacht-properties-in-the-workflow-designer"></a>ParallelForEach<\> 工作流设计器中的属性

下表列出最有用的 <xref:System.Activities.Statements.ParallelForEach%601> 活动属性并说明如何在设计器中使用它们。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定活动设计器在标头中的友好显示名称。 默认值为**ParallelForEach \<Int32> **。 可以在 "**属性**" 网格中或直接在活动设计器标头中编辑该值。|
|<xref:System.Activities.Statements.ParallelForEach%601.Body%2A>|错误|要为集合中的每一项执行的活动。 若要添加 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 活动，请将活动从 "工具箱" 拖放到 " ** \<T> ParallelForEach** " 活动设计器上的 "**正文**" 框中，其中包含提示文本 "将活动放在此处"。|
|**TypeArgument**|正确|<xref:System.Activities.Statements.ParallelForEach%601.Values%2A>由泛型参数*T*指定的集合中的项的类型。默认情况下， **TypeArgument**设置为**Int32**。 若要更改**ParallelForEach<T \> **活动设计器中的类型 T，请在属性网格中更改 " **TypeArgument** " 组合框的值。|
|<xref:System.Activities.Statements.ParallelForEach%601.Values%2A>|正确|要循环访问的项的集合。 若要设置 <xref:System.Activities.Statements.ParallelForEach%601.Values%2A> ，请在 " ** \> ForEach<T** " 活动设计器的 "**值**" 框中，在 "**属性**" 窗口的提示文本 "输入 VB 表达式" 或 "**值**" 框中键入 Visual Basic 表达式。|
|<xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A>||在每个迭代完成后计算。 如果其计算结果为 true，则取消已安排的挂起的迭代。 如果未设置此属性，则所有安排的语句都将执行，直至完成为止。|

默认情况下，循环迭代器是命名项。 可以在 " **ParallelForEach \<T> ** " 活动设计器的 " **ForEach** " 框中更改迭代器变量的名称。 循环迭代器可在 <xref:System.Activities.Statements.ParallelForEach%601> 活动的子级中的表达式中使用。

## <a name="see-also"></a>另请参阅

- [序列](../workflow-designer/sequence-activity-designer.md)
- [Parallel](../workflow-designer/parallel-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)