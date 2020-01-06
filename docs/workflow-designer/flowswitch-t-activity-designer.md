---
title: 工作流设计器-FlowSwitch<T> 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Core.Presentation.FlowSwitchLink.UI
- System.Activities.Statements.FlowSwitch`1.UI
- System.Activities.Core.Presentation.FlowSwitchLink`1.UI
- System.Activities.Core.Presentation.FlowSwitchLinkIdentifier.UI
ms.assetid: 5b9c5afe-7499-4ee8-8c33-28aff14bde07
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8271100936b9cf70e17c0e6279297d583714f018
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75597147"
---
# <a name="flowswitcht-activity-designer"></a>FlowSwitch\<T > 活动设计器

<xref:System.Activities.Statements.FlowSwitch%601> 活动是一个条件节点，它在需要两个以上备选分支时根据匹配条件分支控制流。 如果流分支仅需要两个路径，请改用 <xref:System.Activities.Statements.FlowDecision> 活动。

## <a name="the-flowswitcht-activity"></a>FlowSwitch\<T > 活动

<xref:System.Activities.Statements.FlowSwitch%601> 活动包含一个在计算时返回类型*t* （由泛型参数指定）的值的 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>。 该活动还包含一组 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>，它指定从此计算的可能结果到一组 <xref:System.Activities.Statements.FlowNode> 对象的唯一映射。 执行的 <xref:System.Activities.Statements.FlowNode> 是其类型为*t*的对象与所计算的 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>的值相匹配的对象。 可以选择在没有获得任何匹配时提供 <xref:System.Activities.Statements.FlowSwitch%601.Default%2A> Case。

### <a name="using-the-flowswitcht-activity-designer"></a>使用 FlowSwitch\<T > 活动设计器

可以在 "**工具箱**" 的 "**流程图**" 类别中找到**FlowSwitch\<t >** 活动设计器，通过单击工作流设计器左侧的 **"工具箱**" 选项卡可访问该类别。 或者，从 "**视图**" 菜单中选择 **"工具箱**"，或按**Ctrl**+**Alt**+**X**。

可以将 " **FlowSwitch\<t" >** 活动设计器从 "**工具箱**" 拖放到 "**流程图**" 活动设计器内的工作流设计器图面上。 使用显示的 "**选择类型**" 窗口来指定类型（在代码中与通过其泛型参数 <xref:System.Activities.Statements.FlowSwitch%601> 关联的类型），该类型是从计算 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>中获得的。 此过程在 <xref:System.Activities.Statements.Flowchart>**活动中创建**标记为 "<xref:System.Activities.Statements.FlowSwitch%601>" 的活动。 通过单击提示文本 "输入 VB 表达式" 的位置，可以在 "**属性**" 窗口的 "**表达式**" 框中键入 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>。

将鼠标悬停在**FlowSwitch\<t >** 活动设计器上，使用于链接 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 的正方形控点在其边缘周围显示。 将**FlowSwitch < T\>** 活动设计器和其他活动设计器拖到**流程图**上之后，它们所表示的 <xref:System.Activities.Activity> 对象即可链接在一起以指定执行顺序。 若要创建与 <xref:System.Activities.Statements.FlowSwitch%601>关联的 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 之一，请单击**FlowSwitch < t\>** 外围的一个正方形用例控点，然后将其拖到一个图柄上，当鼠标悬停在其设计器上时，将以类似的方式出现在目标活动附近。 释放鼠标按钮，将显示**FlowSwitch < T\>** 指向目标设计器的箭头，表示此事例。 此情况的默认值显示在箭头上，可在 "**属性**" 窗口的 "**事例**" 框中进行编辑。

### <a name="the-flowswitcht-properties"></a>FlowSwitch\<T > 属性

下表列出 <xref:System.Activities.Statements.FlowSwitch%601> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。

|属性名|必需|用量|
|-|--------------|-|
|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>|True|指定表达式，通过计算该表达式来确定在执行路径中可切换到哪个 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>。|
|<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>|False|指定通过从 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 的可能计算结果到一组 <xref:System.Activities.Statements.FlowNode> 对象的唯一映射。|
|<xref:System.Activities.Statements.FlowSwitch%601.Default%2A>|True|指定当 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 的计算值与 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 对象中包含的值之一不匹配时的映射。|

## <a name="see-also"></a>另请参阅

- [流程图](../workflow-designer/flowchart-activity-designers.md)
- [流程图](../workflow-designer/flowchart-activity-designer.md)
- [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)
