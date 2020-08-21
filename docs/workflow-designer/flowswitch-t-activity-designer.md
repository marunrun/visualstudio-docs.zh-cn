---
title: FlowSwitch &lt; T &gt; 活动设计器工作流设计器
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
ms.openlocfilehash: d6637682bd6ba649f27c1a53f3b1448629f03736
ms.sourcegitcommit: de98ed7edc81383e47b87ae6e61143fbbbe7bc56
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88711568"
---
# <a name="flowswitcht-activity-designer"></a>FlowSwitch\<T> 活动设计器

<xref:System.Activities.Statements.FlowSwitch%601> 活动是一个条件节点，它在需要两个以上备选分支时根据匹配条件分支控制流。 如果流分支仅需要两个路径，请改用 <xref:System.Activities.Statements.FlowDecision> 活动。

## <a name="the-flowswitcht-activity"></a>FlowSwitch \<T> 活动

<xref:System.Activities.Statements.FlowSwitch%601>活动包含一个 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> ，它返回一个类型为*T*的值 (在计算时由泛型参数) 指定。 该活动还包含一组 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>，它指定从此计算的可能结果到一组 <xref:System.Activities.Statements.FlowNode> 对象的唯一映射。 <xref:System.Activities.Statements.FlowNode>执行的是其类型为*T*的对象与所计算的值匹配的对象 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 。 可以选择在没有获得任何匹配时提供 <xref:System.Activities.Statements.FlowSwitch%601.Default%2A> Case。

### <a name="using-the-flowswitcht-activity-designer"></a>使用 FlowSwitch \<T> 活动设计器

" **FlowSwitch \<T> ** " 活动设计器可在 "**工具箱**" 的 "**流程图**" 类别中找到，可通过单击工作流设计器左侧的 "**工具箱**" 选项卡进行访问。 或者，从 "**视图**" 菜单中选择 **"工具箱**"，或按**Ctrl** + **Alt** + **X**。

可以将 " ** \<T> FlowSwitch** " 活动设计器从 "**工具箱**" 拖放到 "**流程图**" 活动设计器内的工作流设计器图面上。 使用显示的 " **选择类型** " 窗口来指定代码中与 (相关联的类型， <xref:System.Activities.Statements.FlowSwitch%601> 其泛型参数) 通过计算得到的 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 。 此过程将 <xref:System.Activities.Statements.FlowSwitch%601> 在活动中创建一个标记为 " **切换** " 的活动 <xref:System.Activities.Statements.Flowchart> 。 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>通过单击提示文本 "输入 VB 表达式" 的位置，可以在 "**属性**" 窗口的 "**表达式**" 框中键入。

将鼠标悬停在 " **FlowSwitch \<T> ** " 活动设计器上会导致用于链接的正方形控点 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 出现在其边缘周围。 将**FlowSwitch<T \> **活动设计器和其他活动设计器拖到**流程图**上之后， <xref:System.Activities.Activity> 它们所表示的对象已准备好链接在一起以指定执行顺序。 若要创建 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 与关联的一个 <xref:System.Activities.Statements.FlowSwitch%601> ，请单击 " **FlowSwitch<T \> ** " 外围网络上的一个正方形控点，然后将鼠标按钮拖动) 到在鼠标悬停在其设计器上时与目标活动类似的方法之一，将其拖 (。 释放鼠标按钮，然后将**FlowSwitch<T \> **中的箭头显示给目标设计器，表示此事例。 此情况的默认值显示在箭头上，可在 "**属性**" 窗口的 "**事例**" 框中进行编辑。

### <a name="the-flowswitcht-properties"></a>FlowSwitch \<T> 属性

下表列出 <xref:System.Activities.Statements.FlowSwitch%601> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>|正确|指定表达式，通过计算该表达式来确定在执行路径中可切换到哪个 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>。|
|<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>|False|指定通过从 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 的可能计算结果到一组 <xref:System.Activities.Statements.FlowNode> 对象的唯一映射。|
|<xref:System.Activities.Statements.FlowSwitch%601.Default%2A>|正确|指定当 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 的计算值与 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 对象中包含的值之一不匹配时的映射。|

## <a name="see-also"></a>另请参阅

- [流程图](../workflow-designer/flowchart-activity-designers.md)
- [流程图](../workflow-designer/flowchart-activity-designer.md)
- [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)
