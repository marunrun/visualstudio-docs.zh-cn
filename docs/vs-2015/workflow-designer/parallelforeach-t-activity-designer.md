---
title: ParallelForEach &lt;T &gt; 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ParallelForEach`1.UI
ms.assetid: e93a4843-aef2-4d3e-9a0a-a2d3d1411aa7
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4c659e941a8503a0d5ff601fea23fcec69b2bbcf
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672604"
---
# <a name="parallelforeachlttgt-activity-designer"></a>ParallelForEach &lt;T &gt; 活动设计器
<xref:System.Activities.Statements.ParallelForEach%601> 活动枚举集合元素并对集合中的每个元素并行执行嵌入语句，这将在同一线程上异步执行。 如果此活动的子活动预期会进入空闲状态，请使用此流控制活动，而不是 <xref:System.Activities.Statements.Sequence> 活动。

 <xref:System.Activities.Statements.ParallelForEach%601> 活动有一个 <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> 属性，该属性包含用户指定的 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 表达式。 <xref:System.Activities.Statements.ParallelForEach%601> 活动在完成每个分支后计算此属性。 如果计算结果为**true**，则 <xref:System.Activities.Statements.ParallelForEach%601> 活动完成，而不执行其他分支。 如果 <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> 的计算结果不为**true**，则在完成其所有子活动后 <xref:System.Activities.Statements.ParallelForEach%601> 活动完成。

## <a name="the-parallelforeacht-activity"></a>ParallelForEach \<T > 活动
 <xref:System.Activities.Statements.ParallelForEach%601> 枚举其值并为枚举的每个值安排 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 的执行顺序。 仅安排 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 的执行顺序。 Body 的执行方式取决于 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 是否进入空闲状态。

 如果 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 未进入空闲状态，则会按相反顺序执行，因为安排的活动作为堆栈来处理，最后安排的活动最先执行。 例如，如果您有一个 {1,2,3,4}in 的集合 <xref:System.Activities.Statements.ParallelForEach%601> 并使用**WriteLine**作为主体来写入值。已在控制台中打印4、3、2、1。 这是因为， **WriteLine**不会处于空闲状态，因此在计划4个**writeline**活动后，将使用堆栈行为（在最后一个结束时）执行该操作。

 但是如果 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 中有会进入空闲状态的活动，如 <xref:System.ServiceModel.Activities.Receive> 活动或 <xref:System.Activities.Statements.Delay> 活动， 那么就不需要等待它们完成。 <xref:System.Activities.Statements.ParallelForEach%601> 转至下一个预定的主体活动，并尝试执行它。 如果该活动也进入空闲状态，则 <xref:System.Activities.Statements.ParallelForEach%601> 将再移到下一个 Body 活动。

### <a name="using-the-parallelforeacht-activity-designer"></a>使用 ParallelForEach \<T > 活动设计器
 **ParallelForEach \<T >** 活动设计器可在 "**工具箱**" 的 "**控制流**" 类别中找到，该类别可通过单击 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 左侧的 "**工具箱**" 选项卡进行访问（或者，也可以选择"**视图**" 菜单中的工具栏，或按 CTRL + ALT + X。）

 可以将 " **ParallelForEach \<T >** 活动设计器从"**工具箱**"拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动设计器的任何位置，例如，在" **Sequence** "活动设计器内。 将其放入 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 后，它将创建一个 <xref:System.Activities.Statements.ParallelForEach%601> 活动，该活动在默认情况下包含**ParallelForEach \<Int32 >** 的 <xref:System.Activities.Activity.DisplayName%2A>。

### <a name="parallelforeacht-properties-in-the-workflow-designer"></a>ParallelForEach \<T 工作流设计器中 > 属性
 下表列出最有用的 <xref:System.Activities.Statements.ParallelForEach%601> 活动属性并说明如何在设计器中使用它们。

|属性名|必需|用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定活动设计器在标头中的友好显示名称。 默认值为**ParallelForEach \<Int32 >** 。 可以在 "**属性**" 网格中或直接在活动设计器标头中编辑该值。|
|<xref:System.Activities.Statements.ParallelForEach%601.Body%2A>|False|要为集合中的每一项执行的活动。 若要添加 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 活动，请将活动从 "工具箱" 拖放到 " **ParallelForEach" \<T**上的 "**正文**" 框中 > "活动设计器"，并在提示文本 "将活动放在此处"|
|**TypeArgument**|True|泛型参数*t*指定的 <xref:System.Activities.Statements.ParallelForEach%601.Values%2A> 集合中的项的类型。默认情况下， **TypeArgument**设置为**Int32**。 若要更改 " **ParallelForEach \<T >** " 活动设计器中的类型 T，请在属性网格中更改 " **TypeArgument** " 组合框的值。|
|<xref:System.Activities.Statements.ParallelForEach%601.Values%2A>|True|要循环访问的项的集合。 若要设置 <xref:System.Activities.Statements.ParallelForEach%601.Values%2A>，请在 " **ForEach \<T >** 活动设计器" 的 "**值**" 框中，在 "**属性**" 窗口的提示文本 "输入 VB 表达式" 或 "**值**" 框中键入 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 表达式。|
|<xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A>||在每个迭代完成后计算。 如果其计算结果为 true，则取消已安排的挂起的迭代。 如果未设置此属性，则所有安排的语句都将执行，直至完成为止。|

 默认情况下，循环迭代器是命名项。 可以在 " **ParallelForEach \<T >** " 活动设计器的 " **ForEach** " 框中更改迭代器变量的名称。 循环迭代器可在 <xref:System.Activities.Statements.ParallelForEach%601> 活动的子级中的表达式中使用。

## <a name="see-also"></a>请参阅
 [序列](../workflow-designer/sequence-activity-designer.md)[并行](../workflow-designer/parallel-activity-designer.md)[控制流](../workflow-designer/control-flow-activity-designers.md)