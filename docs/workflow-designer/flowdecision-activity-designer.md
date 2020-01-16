---
title: 工作流设计器 FlowDecision 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.FlowDecision.UI
ms.assetid: 4a49edc3-3662-4b7b-812e-0a5ba00d6c94
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 79e405f82bcf33bc01ad07f1092879c17dec5849
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76111435"
---
# <a name="flowdecision-activity-designer"></a>FlowDecision 活动设计器

<xref:System.Activities.Statements.FlowDecision> 节点是一个条件节点，它根据指定条件是否成立来将控制流分支到两个备分支之一。 如果流需要的分支超过两个，请改用 <xref:System.Activities.Statements.FlowSwitch%601>。

## <a name="the-flowdecision-node"></a>FlowDecision 节点

当流可以分支到两条路径时可使用 <xref:System.Activities.Statements.FlowDecision>。 一个 <xref:System.Activities.Statements.FlowDecision> 节点具有一个 <xref:System.Activities.Statements.FlowDecision.Condition%2A>，并且两个可能结果中的每一个都有一个关联的 <xref:System.Activities.Statements.FlowNode>，这两个可能的结果为：<xref:System.Activities.Statements.FlowDecision.True%2A> 和 <xref:System.Activities.Statements.FlowDecision.False%2A>。 将对 <xref:System.Activities.Statements.FlowDecision.Condition%2A> 进行计算，此计算值决定要在 <xref:System.Activities.Statements.FlowNode> 中处理的下一个 <xref:System.Activities.Statements.Flowchart>。

### <a name="using-the-flowdecision-designer"></a>使用 FlowDecision 设计器

**FlowDecision**设计器可在 "**工具箱**" 的 "**流程图**" 类别中找到，可通过单击工作流设计器上的 "**工具箱**" 选项卡进行访问。 或者，从 "**视图**" 菜单中选择 **"工具箱**"，或按**Ctrl**+**Alt**+**X**。

可以将 " **FlowDecision** " 设计器从 "**工具箱**" 拖放到 "**流程图**" 活动设计器内的工作流设计器图面上。 这**会在 <xref:System.Activities.Statements.Flowchart> 活动中创建**一个标记为 "<xref:System.Activities.Statements.FlowDecision>" 的标记。 将鼠标悬停在设计器上，将显示两个分支的**True**和**False**方控点。

将**FlowDecision**设计器和其他设计器拖到**Flowchart**后，可将节点链接在一起以指定执行顺序。 若要在源节点（包括**FlowDecision**的**True**和**False**分支）和目标节点之间创建链接，请将鼠标悬停在源节点的设计器上，并在其每一侧显示正方形控点。 单击这些正方形处理框之一并按下鼠标按钮将其拖到当鼠标悬停在目标节点上时该节点周围以类似方式显示的处理框之一。 松开鼠标按钮，此时将在这两个节点之间创建一个链接，表示为从源设计器指向目标设计器的箭头。

通过单击提示文本 "输入 VB 表达式" 的位置，可以在 "**属性**" 窗口的 "**条件**" 框中键入指明 <xref:System.Activities.Statements.FlowDecision.Condition%2A> 的表达式。

### <a name="the-flowdecision-properties"></a>FlowDecision 属性

下表列出 <xref:System.Activities.Statements.FlowDecision> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。

|属性名|必需|用量|
|-|--------------|-|
|<xref:System.Activities.Statements.FlowDecision.Condition%2A>|True|确定流控制所采用的路径的条件。|
|<xref:System.Activities.Statements.FlowDecision.True%2A>|False|<xref:System.Activities.Statements.FlowDecision.Condition%2A> 成立时流控制所采用的路径。|
|<xref:System.Activities.Statements.FlowDecision.False%2A>|False|<xref:System.Activities.Statements.FlowDecision.Condition%2A> 不成立时流控制所采用的路径。|

## <a name="see-also"></a>另请参阅

- [流程图](../workflow-designer/flowchart-activity-designers.md)
- [流程图](../workflow-designer/flowchart-activity-designer.md)
- [FlowSwitch\<T>](../workflow-designer/flowswitch-t-activity-designer.md)
