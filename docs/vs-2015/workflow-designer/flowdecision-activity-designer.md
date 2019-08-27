---
title: FlowDecision 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.FlowDecision.UI
ms.assetid: 4a49edc3-3662-4b7b-812e-0a5ba00d6c94
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 46ff7dc7ae79ae8bf269a7a3d3cad780ad7654bb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62943355"
---
# <a name="flowdecision-activity-designer"></a>FlowDecision 活动设计器
<xref:System.Activities.Statements.FlowDecision> 节点是一个条件节点，它根据指定条件是否成立来将控制流分支到两个备分支之一。 如果流需要的分支超过两个，请改用 <xref:System.Activities.Statements.FlowSwitch%601>。  
  
## <a name="the-flowdecision-node"></a>FlowDecision 节点  
 当流可以分支到两条路径时可使用 <xref:System.Activities.Statements.FlowDecision>。 一个 <xref:System.Activities.Statements.FlowDecision> 节点具有一个 <xref:System.Activities.Statements.FlowDecision.Condition%2A>，并且两个可能结果中的每一个都有一个关联的 <xref:System.Activities.Statements.FlowNode>，这两个可能的结果为：<xref:System.Activities.Statements.FlowDecision.True%2A> 和 <xref:System.Activities.Statements.FlowDecision.False%2A>。 将对 <xref:System.Activities.Statements.FlowDecision.Condition%2A> 进行计算，此计算值决定要在 <xref:System.Activities.Statements.FlowNode> 中处理的下一个 <xref:System.Activities.Statements.Flowchart>。  
  
### <a name="using-the-flowdecision-designer"></a>使用 FlowDecision 设计器  
 **FlowDecision**设计器可在**流程图**类别**工具箱**，这通过单击来访问**工具箱**选项卡上[!INCLUDE[wfd2](../includes/wfd2-md.md)](或者，选择**工具栏**从**视图**菜单或 CTRL + ALT + X。)  
  
 **FlowDecision**设计器可以从拖动**工具箱**拖放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面中**流程图**活动设计器。 这将创建<xref:System.Activities.Statements.FlowDecision>标记为**决策**内<xref:System.Activities.Statements.Flowchart>活动。 鼠标悬停在设计器和 **，则返回 True**并**False**显示正方形处理框的两个分支。  
  
 之后**FlowDecision**设计器和其他设计器拖到**流程图**，节点可以链接在一起以指定执行顺序。 若要创建的源节点之间的链接 (包括 **，则返回 True**并**False**的分支**FlowDecision**) 和一个目标节点，鼠标悬停在设计器的源节点它的每一侧显示正方形处理框。 单击这些正方形处理框之一并按下鼠标按钮将其拖到当鼠标悬停在目标节点上时该节点周围以类似方式显示的处理框之一。 松开鼠标按钮，此时将在这两个节点之间创建一个链接，表示为从源设计器指向目标设计器的箭头。  
  
 表达式，指出<xref:System.Activities.Statements.FlowDecision.Condition%2A>可以在类型化**条件**的框**属性**窗口可通过单击提示文本显示"输入 VB 表达式"。  
  
### <a name="the-flowdecision-properties"></a>FlowDecision 属性  
 下表列出 <xref:System.Activities.Statements.FlowDecision> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Statements.FlowDecision.Condition%2A>|True|确定流控制所采用的路径的条件。|  
|<xref:System.Activities.Statements.FlowDecision.True%2A>|False|<xref:System.Activities.Statements.FlowDecision.Condition%2A> 成立时流控制所采用的路径。|  
|<xref:System.Activities.Statements.FlowDecision.False%2A>|False|<xref:System.Activities.Statements.FlowDecision.Condition%2A> 不成立时流控制所采用的路径。|  
  
## <a name="see-also"></a>请参阅  
 [流程图](../workflow-designer/flowchart-activity-designers.md)   
 [流程图](../workflow-designer/flowchart-activity-designer.md)   
 [FlowSwitch\<T>](../workflow-designer/flowswitch-t-activity-designer.md)