---
title: StateMachine 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- StateMachine Designer
- System.Activities.Statements.StateMachine.UI
ms.assetid: 474d5fb3-1049-4b3f-bc6b-7524dbbe1672
caps.latest.revision: 5
author: steved0x
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5fc9d34e06ca443b39a1a57aa88fee1155f47a8c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660107"
---
# <a name="statemachine-activity-designer"></a>StateMachine 活动设计器
<xref:System.Activities.Statements.StateMachine> 活动包含使用熟悉的状态机范式的状态和模型工作流的集合。

## <a name="using-the-statemachine-activity-designer"></a>使用 StateMachine 活动设计器
 若要添加 <xref:System.Activities.Statements.StateMachine> 活动，请将 " **StateMachine** " 活动设计器从 "**工具箱**" 的 "**状态机**" 部分拖放到 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 图面上。 若要将子状态添加到此 <xref:System.Activities.Statements.StateMachine> 活动，请从 "**工具箱**" 中拖动 <xref:System.Activities.Statements.State> 或 <xref:System.Activities.Core.Presentation.FinalState>，并将其放到**StateMachine**上。

### <a name="statemachine-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 StateMachine 活动属性
 下表列出可使用工作流设计器设置的 <xref:System.Activities.Statements.StateMachine> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在设计器图面上进行编辑。

|属性名|必需|用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.StateMachine> 活动设计器在标头中的友好名称。 默认值为**StateMachine**。 可以在属性网格或直接在活动设计器的标头中编辑该值。 <xref:System.Activities.Activity.DisplayName%2A> 用于痕迹导航，后者显示在工作流设计器顶部。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|

## <a name="see-also"></a>请参阅
 [流程图](../workflow-designer/flowchart-activity-designer.md)[控制流](../workflow-designer/control-flow-activity-designers.md)