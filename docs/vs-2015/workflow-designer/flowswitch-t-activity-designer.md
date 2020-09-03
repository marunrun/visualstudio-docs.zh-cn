---
title: FlowSwitch &lt; T &gt; 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Core.Presentation.FlowSwitchLink.UI
- System.Activities.Statements.FlowSwitch`1.UI
- System.Activities.Core.Presentation.FlowSwitchLink`1.UI
- System.Activities.Core.Presentation.FlowSwitchLinkIdentifier.UI
ms.assetid: 5b9c5afe-7499-4ee8-8c33-28aff14bde07
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 27abb660766a7c04742eca221432af19f05f0d28
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656647"
---
# <a name="flowswitchlttgt-activity-designer"></a>FlowSwitch &lt; T &gt; 活动设计器
<xref:System.Activities.Statements.FlowSwitch%601> 活动是一个条件节点，它在需要两个以上备选分支时根据匹配条件分支控制流。 如果流分支仅需要两个路径，请改用 <xref:System.Activities.Statements.FlowDecision> 活动。

## <a name="the-flowswitcht-activity"></a>FlowSwitch \<T> 活动
 <xref:System.Activities.Statements.FlowSwitch%601>活动包含一个 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> ，它返回一个类型为*T*的值 (在计算时由泛型参数) 指定。 该活动还包含一组 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>，它指定从此计算的可能结果到一组 <xref:System.Activities.Statements.FlowNode> 对象的唯一映射。 <xref:System.Activities.Statements.FlowNode>执行的是其类型为*T*的对象与所计算的值匹配的对象 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 。 可以选择在没有获得任何匹配时提供 <xref:System.Activities.Statements.FlowSwitch%601.Default%2A> Case。

### <a name="using-the-flowswitcht-activity-designer"></a>使用 FlowSwitch \<T> 活动设计器
 " **FlowSwitch \<T> ** " 活动设计器可在 "**工具箱**" 的 "**流程图**" 类别中找到，可通过单击 (左侧的 "**工具箱**" 选项卡进行访问 [!INCLUDE[wfd2](../includes/wfd2-md.md)] ，也可以从 "**视图**" 菜单中选择 "**工具栏**" 或按 CTRL + ALT + X。 ) 

 可以将 " ** \<T> FlowSwitch** " 活动设计器从 "**工具箱**" 拖放到图面上的 " [!INCLUDE[wfd2](../includes/wfd2-md.md)] **流程图**" 活动设计器中。 使用显示的 " **选择类型** " 窗口来指定代码中与 (相关联的类型， <xref:System.Activities.Statements.FlowSwitch%601> 其泛型参数) 通过计算得到的 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 。 此过程将 <xref:System.Activities.Statements.FlowSwitch%601> 在活动中创建一个标记为 " **切换** " 的活动 <xref:System.Activities.Statements.Flowchart> 。 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>通过单击提示文本 "输入 VB 表达式" 的位置，可以在 "**属性**" 窗口的 "**表达式**" 框中键入。

 将鼠标悬停在 " **FlowSwitch \<T> ** " 活动设计器上会导致用于链接的正方形控点 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 出现在其边缘周围。 将**FlowSwitch<T \> **活动设计器和其他活动设计器拖到**流程图**上之后， <xref:System.Activities.Activity> 它们所表示的对象已准备好链接在一起以指定执行顺序。 若要创建 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 与关联的一个 <xref:System.Activities.Statements.FlowSwitch%601> ，请在**FlowSwitch \<T> **的外围上单击其中一个方块控点，并将其拖 (方法：按住鼠标按钮，将) 到在鼠标悬停在其设计器上时，与目标活动类似的方法之一。 松开鼠标按钮，此时将显示一个从**FlowSwitch \<T> **到目标设计器的箭头，用于表示此事例。 此情况的默认值显示在箭头上，可在 "**属性**" 窗口的 "**事例**" 框中进行编辑。

### <a name="the-flowswitcht-properties"></a>FlowSwitch \<T> 属性
 下表列出 <xref:System.Activities.Statements.FlowSwitch%601> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-------------------|--------------|-----------|
|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>|正确|指定表达式，通过计算该表达式来确定在执行路径中可切换到哪个 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>。|
|<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>|错误|指定通过从 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 的可能计算结果到一组 <xref:System.Activities.Statements.FlowNode> 对象的唯一映射。|
|<xref:System.Activities.Statements.FlowSwitch%601.Default%2A>|正确|指定当 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 的计算值与 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 对象中包含的值之一不匹配时的映射。|

## <a name="see-also"></a>另请参阅
 [流程图](../workflow-designer/flowchart-activity-designers.md) [Flowchart](../workflow-designer/flowchart-activity-designer.md) [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)