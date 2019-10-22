---
title: 工作流设计器-Flowchart 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Flowchart.UI
- System.Activities.Statements.FlowStep.UI
- System.Activities.Core.Presentation.FlowStart.UI
ms.assetid: d5af2276-5215-4138-880a-cf2b90bbf3a0
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5f56c7eac56572d8a3be1f8b478feb0543390481
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650461"
---
# <a name="flowchart-activity-designer"></a>流程图活动设计器

<xref:System.Activities.Statements.Flowchart> 活动用于创建定义和管理复杂流控制的工作流。 可以通过代码或使用工作流设计器创作 <xref:System.Activities.Statements.Flowchart>。 本主题介绍工作流设计器体验。 使用工作流设计器工作流活动设计器，开发人员可通过自然方式创作工作流。

## <a name="the-flowchart-activity"></a>Flowchart 活动

<xref:System.Activities.Statements.Flowchart> 指定工作流启动时执行的唯一 <xref:System.Activities.Statements.Flowchart.StartNode%2A>，并使用链接的 <xref:System.Activities.Statements.Flowchart.Nodes%2A> 网络创建任意循环或将执行流在任意给定时间转移到工作流中的其他任何位置。

### <a name="using-the-flowchart-activity-designer"></a>使用 Flowchart 活动设计器

" **Flowchart** " 活动设计器可在 "**工具箱**" 的 "**流程图**" 类别中找到，可通过单击工作流设计器上的 "**工具箱**" 选项卡进行访问。 或者，从 "**视图**" 菜单中选择 **"工具箱**"，或按**Ctrl** +**Alt** +**X**。

**Flowchart**活动设计器可以从 "**工具箱**" 拖放到工作流设计器图面上通常放置活动设计器的任何位置，要么作为根活动，要么作为另一个控制流活动的子活动。 如果将 " **Flowchart** " 活动设计器放到空白工作流设计器图面上，则它会创建一个 <xref:System.Activities.Statements.Flowchart> 活动，该活动默认情况下显示在展开的视图中，启动执行的开始节点表示为绿色球。 如果将 " **flowchart** " 活动设计器放入另一个控制流活动，则它将显示在可通过双击**Flowchart**活动设计器展开的最小化视图中。 **工具箱**中的任何活动都可以直接拖到**Flowchart**活动设计器中，包括其他控制流活动。

将各种活动设计器拖动到工作流设计器画布上之后，它们所表示的 <xref:System.Activities.Activity> 对象可以链接在一起以指定执行顺序。 若要在源活动与目标活动之间创建链接，请将鼠标悬停在源活动的设计器上，此时将在该设计器的每一侧显示正方形处理框。 单击这些正方形处理框之一并按下鼠标按钮将其拖到当鼠标悬停在目标活动上时该活动周围以类似方式显示的处理框之一。 松开鼠标按钮，此时将在这两个活动之间创建一个链接，表示为从源设计器指向目标设计器的箭头。

### <a name="flowchart-activity-properties"></a>Flowchart 活动属性

下表列出 <xref:System.Activities.Statements.Flowchart> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定活动设计器在标头中的显示名称。 默认值为 Flowchart。 该值可以在 "**属性**" 窗口中编辑，也可以直接在活动设计器标头中编辑。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.Flowchart.Variables%2A>|False|作用范围在此 <xref:System.Activities.Statements.Flowchart> 内以在其子活动间共享状态的变量的集合。|
|<xref:System.Activities.Statements.Flowchart.StartNode%2A>|False|在 <xref:System.Activities.Statements.FlowNode> 启动时执行的 <xref:System.Activities.Statements.Flowchart>。|
|<xref:System.Activities.Statements.Flowchart.Nodes%2A>|False|包含 <xref:System.Activities.Statements.FlowNode> 中的 <xref:System.Activities.Statements.Flowchart> 对象的集合。|

## <a name="see-also"></a>请参阅

- [流程图](../workflow-designer/flowchart-activity-designers.md)
- [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)
- [FlowSwitch\<T>](../workflow-designer/flowswitch-t-activity-designer.md)