---
title: FlowSwitch&lt;T&gt;活动设计器 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ccd3e328a904540dd03c85f53634dc1eaab96c6e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62943302"
---
# <a name="flowswitchlttgt-activity-designer"></a>FlowSwitch&lt;T&gt;活动设计器
<xref:System.Activities.Statements.FlowSwitch%601> 活动是一个条件节点，它在需要两个以上备选分支时根据匹配条件分支控制流。 如果流分支仅需要两个路径，请改用 <xref:System.Activities.Statements.FlowDecision> 活动。  
  
## <a name="the-flowswitcht-activity"></a>FlowSwitch\<T > 活动  
 <xref:System.Activities.Statements.FlowSwitch%601>活动包含<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>返回类型的值*T* （由泛型参数指定） 评估时。 该活动还包含一组 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>，它指定从此计算的可能结果到一组 <xref:System.Activities.Statements.FlowNode> 对象的唯一映射。 <xref:System.Activities.Statements.FlowNode>执行对象的类型是一个*T*是计算得到的值匹配<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>。 可以选择在没有获得任何匹配时提供 <xref:System.Activities.Statements.FlowSwitch%601.Default%2A> Case。  
  
### <a name="using-the-flowswitcht-activity-designer"></a>使用 FlowSwitch\<T > 活动设计器  
 **FlowSwitch\<T >** 活动设计器可在**流程图**类别**工具箱**，这通过单击访问**工具箱**选项卡的左侧[!INCLUDE[wfd2](../includes/wfd2-md.md)](或者，选择**工具栏**从**视图**菜单或 CTRL + ALT + X。)  
  
 **FlowSwitch\<T >** 活动设计器可以从拖动**工具箱**拖放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]面内**流程图**活动设计器。 使用**选择类型**窗口，其中显示指定的类型 (在代码中使用相关联<xref:System.Activities.Statements.FlowSwitch%601>通过其泛型参数) 从评估中获得<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>。 此过程创建<xref:System.Activities.Statements.FlowSwitch%601>标记为活动**交换机**内<xref:System.Activities.Statements.Flowchart>活动。 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>可以在类型化**表达式**的框**属性**窗口可通过单击提示文本显示"输入 VB 表达式"。  
  
 将鼠标移到**FlowSwitch\<T >** 活动设计器会导致用于链接的正方形处理<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>其边缘周围出现。 之后**FlowSwitch < T\>** 活动设计器和其他活动设计器拖到**流程图**，则<xref:System.Activities.Activity>它们所表示的对象已准备好链接在一起若要指定的执行顺序。 若要创建的一个<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>与相关联<xref:System.Activities.Statements.FlowSwitch%601>，单击其中一个的外围网络上的正方形 case 处理**FlowSwitch\<T >** 并将其拖到一个句柄的 （通过按下鼠标按钮）当鼠标悬停在其设计器时显示在目标活动周围以类似方式。 松开鼠标按钮，从一个箭头**FlowSwitch\<T >** 指向目标设计器将显示表示此 case。 默认值为这种情况下显示的箭头，并可以在对其进行编辑**用例**的框**属性**窗口。  
  
### <a name="the-flowswitcht-properties"></a>FlowSwitch\<T > 属性  
 下表列出 <xref:System.Activities.Statements.FlowSwitch%601> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>|True|指定表达式，通过计算该表达式来确定在执行路径中可切换到哪个 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>。|  
|<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>|False|指定通过从 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 的可能计算结果到一组 <xref:System.Activities.Statements.FlowNode> 对象的唯一映射。|  
|<xref:System.Activities.Statements.FlowSwitch%601.Default%2A>|True|指定当 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 的计算值与 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 对象中包含的值之一不匹配时的映射。|  
  
## <a name="see-also"></a>请参阅  
 [流程图](../workflow-designer/flowchart-activity-designers.md)   
 [流程图](../workflow-designer/flowchart-activity-designer.md)   
 [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)