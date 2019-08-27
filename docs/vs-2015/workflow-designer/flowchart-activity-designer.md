---
title: 流程图活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Flowchart.UI
- System.Activities.Statements.FlowStep.UI
- System.Activities.Core.Presentation.FlowStart.UI
ms.assetid: d5af2276-5215-4138-880a-cf2b90bbf3a0
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 3e89caded1b7388b79ea3232dc0a2809dc7b8222
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62943474"
---
# <a name="flowchart-activity-designer"></a>流程图活动设计器
<xref:System.Activities.Statements.Flowchart> 活动用于创建定义和管理复杂流控制的工作流。 可以使用代码或 <xref:System.Activities.Statements.Flowchart> 创作 [!INCLUDE[wfd2](../includes/wfd2-md.md)]。 本主题讲述 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 体验。 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 工作流活动设计器使开发人员能够以自然的方式创作工作流。  
  
## <a name="the-flowchart-activity"></a>Flowchart 活动  
 <xref:System.Activities.Statements.Flowchart> 指定工作流启动时执行的唯一 <xref:System.Activities.Statements.Flowchart.StartNode%2A>，并使用链接的 <xref:System.Activities.Statements.Flowchart.Nodes%2A> 网络创建任意循环或将执行流在任意给定时间转移到工作流中的其他任何位置。  
  
### <a name="using-the-flowchart-activity-designer"></a>使用 Flowchart 活动设计器  
 **流程图**活动设计器可在**流程图**类别**工具箱**，这通过单击来访问**工具箱**选项卡上[!INCLUDE[wfd2](../includes/wfd2-md.md)](或者，选择**工具栏**从**视图**菜单或 CTRL + ALT + X。)  
  
 **流程图**活动设计器可以从拖动**工具箱**拖放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面上活动设计器放置的任何位置通常情况下，作为根活动或作为子级另一个控制流活动。 如果**流程图**活动设计器放到一个空白[!INCLUDE[wfd2](../includes/wfd2-md.md)]面上，它会创建<xref:System.Activities.Statements.Flowchart>活动，在其中启动执行的开始节点是展开的视图以显示本身默认情况下的表示为一个绿球。 如果**流程图**活动设计器拖放到另一个控制流活动，它可以通过双击扩展的最小化视图中提供本身**流程图**活动设计器。 中的任何活动**工具箱**可以直接拖到拖放**流程图**活动设计器中，包括其他控制流活动。  
  
 将各种活动设计器拖到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 画布上之后，这些活动设计器表示的 <xref:System.Activities.Activity> 对象可链接在一起以指定执行顺序。 若要在源活动与目标活动之间创建链接，请将鼠标悬停在源活动的设计器上，此时将在该设计器的每一侧显示正方形处理框。 单击这些正方形处理框之一并按下鼠标按钮将其拖到当鼠标悬停在目标活动上时该活动周围以类似方式显示的处理框之一。 松开鼠标按钮，此时将在这两个活动之间创建一个链接，表示为从源设计器指向目标设计器的箭头。  
  
### <a name="flowchart-activity-properties"></a>Flowchart 活动属性  
 下表列出 <xref:System.Activities.Statements.Flowchart> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定活动设计器在标头中的显示名称。 默认值为 Flowchart。 可以在编辑该值**属性**窗口或直接在活动设计器标头。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|  
|<xref:System.Activities.Statements.Flowchart.Variables%2A>|False|作用范围在此 <xref:System.Activities.Statements.Flowchart> 内以在其子活动间共享状态的变量的集合。|  
|<xref:System.Activities.Statements.Flowchart.StartNode%2A>|False|在 <xref:System.Activities.Statements.FlowNode> 启动时执行的 <xref:System.Activities.Statements.Flowchart>。|  
|<xref:System.Activities.Statements.Flowchart.Nodes%2A>|False|包含 <xref:System.Activities.Statements.FlowNode> 中的 <xref:System.Activities.Statements.Flowchart> 对象的集合。|  
  
## <a name="see-also"></a>请参阅  
 [流程图](../workflow-designer/flowchart-activity-designers.md)   
 [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)   
 [FlowSwitch\<T>](../workflow-designer/flowswitch-t-activity-designer.md)