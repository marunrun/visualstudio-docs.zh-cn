---
title: 转换活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Transition.UI
ms.assetid: f6e8b5cc-7fb8-4699-9703-f3c9fc7cc316
caps.latest.revision: 7
author: steved0x
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 026ee7af3c60b3832449f5f2ed996f00c75a1c87
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435382"
---
# <a name="transition-activity-designer"></a>事务活动设计器
<xref:System.Activities.Statements.Transition> 表示两个状态间的转换。  
  
## <a name="using-the-transition-activity-designer"></a>使用 Transition 活动设计器  
 Transition 活动设计器允许您在两个状态之间配置转换。  
  
### <a name="transition-properties-in-the-workflow-designer"></a>工作流设计器中的 Transition 属性  
 下表列出可使用工作流设计器设置的 <xref:System.Activities.Statements.Transition> 属性并说明如何在设计器中使用它们。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Statements.Transition.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.Transition> 活动设计器的友好名称。 默认值是**T1**。 可在属性网格、扩展转换设计器的标题以及扩展转换设计器内的操作部分的标题中编辑值。 <xref:System.Activities.Activity.DisplayName%2A> 用于痕迹导航，后者显示在工作流设计器顶部。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|  
|<xref:System.Activities.Statements.Transition.Condition%2A>|False|如果存在，请指定一个表达式，计算结果必须为 **，则返回 True**控制权将传递给目标状态之前。 可以在属性网格和扩展转换设计器中编辑此条件。 共享转换中的多个条件按显示在转换设计器中的顺序进行评估。 **注意：** 请注意，如果<xref:System.Activities.Statements.Transition.Condition%2A>转换的计算结果为**False** (或所有共享的触发转换条件的计算结果为**False**)，将不会进行转换和所有的所有触发器从状态转换将重新安排。 在本教程中，由于配置条件的方式，这种情况不会发生（我们针对猜测是正确或者错误提供了具体的操作）。|  
|**源**|True|指示源自此转换的状态。 单击源状态的名称可将设计器视图切换到状态的扩展视图。 在创建转换时设置此值，并且不能更改它。|  
|<xref:System.Activities.Statements.Transition.Trigger%2A>|False|指定其完成启动转换的活动。 若要设置此活动，请将活动从拖**工具箱**并将其拖到放置**触发器**过渡的部分。|  
|<xref:System.Activities.Statements.Transition.Action%2A>|False|指定触发器活动完成时执行的活动和<xref:System.Activities.Statements.Transition.Condition%2A>(如果有） 的计算结果为**true**。 在源状态的 <xref:System.Activities.Statements.State.Exit%2A> 活动后、转换到目标状态时执行此活动，如果存在，则执行。 扩展转换设计器时，可以通过拖动将活动从设置该值**工具箱**并将其放置到**操作**过渡的部分。 单个转换可对应多个操作。 可以展开和收缩各个操作，在转换中存在多个操作时可通过单击在操作上显示的向上或向下箭头键进行排序。|  
|**目标**|True|指示转换完成后状态计算机转换到的状态。 这与对象模型中转换的 <xref:System.Activities.Statements.Transition.To%2A> 属性相对应。 单击目标状态的名称可将设计器视图切换到状态的扩展视图。 在创建转换时设置此值，并可以通过拖动将转换连接到设计器中的目标状态的箭头进行更改。|  
  
### <a name="creating-transitions"></a>创建转换  
 通过将某行从一个状态拖到另一个状态，或在从一个状态拖动到另一个状态时通过将状态拖放到出现的三角形上，来创建转换。 若要通过拖动来创建转换，请将鼠标悬停在源状态的边缘，并将某行从源状态拖到目标状态。 若要通过拖放方式创建转换，请拖动目标状态并将其悬停在源状态，将它拖到源状态周围显示的四个三角形之一。 目标状态可以是从的新状态**工具箱**，或从工作流设计器中拖动的现有状态。  
  
> [!NOTE]
> 状态机中的单个状态使用工作流设计器可以创建多达 76 个转换。 对在设计器外创建的工作流状态的转换限制只受系统资源限制。  
  
 共享触发器转换是共享相同的触发事件的一组转换。 共享触发器基于为共享公用触发器事件的多个转换配置的表达式评估结果，允许有条件转换到目标状态。 若要将其他操作添加到转换和创建共享转换，请单击指示所需转换的开始的圆并将它拖到所需的状态。 新转换将与初始转换共享相同的触发器，但它将具有一个唯一的条件和操作。 共享的转换还可以创建从在转换设计器通过单击**添加共享的触发器转换**底部的转换设计器，然后选择所需的目标状态从**若要连接的可用状态**下拉列表。  
  
## <a name="see-also"></a>请参阅  
 [StateMachine](../workflow-designer/statemachine-activity-designer.md)   
 [FinalState](../workflow-designer/finalstate-activity-designer.md)   
 [状态](../workflow-designer/state-activity-designer.md)