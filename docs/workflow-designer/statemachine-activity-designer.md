---
title: 工作流设计器-StateMachine 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- StateMachine Designer
- System.Activities.Statements.StateMachine.UI
ms.assetid: 474d5fb3-1049-4b3f-bc6b-7524dbbe1672
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 59b1a194f4f301bd3080820b56c89044315c66e7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62809388"
---
# <a name="statemachine-activity-designer"></a>StateMachine 活动设计器

<xref:System.Activities.Statements.StateMachine> 活动包含使用熟悉的状态机范式的状态和模型工作流的集合。

## <a name="using-the-statemachine-activity-designer"></a>使用 StateMachine 活动设计器

若要添加<xref:System.Activities.Statements.StateMachine>活动，请将**StateMachine**活动设计器从**状态机**一部分**工具箱**拖放到工作流设计器图面。 若要将子状态添加到此<xref:System.Activities.Statements.StateMachine>活动，请将<xref:System.Activities.Statements.State>或<xref:System.Activities.Core.Presentation.FinalState>从**工具箱**并将其拖到放置**StateMachine**。

### <a name="statemachine-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 StateMachine 活动属性

下表列出可使用工作流设计器设置的 <xref:System.Activities.Statements.StateMachine> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在设计器图面上进行编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.StateMachine> 活动设计器在标头中的友好名称。 默认值是**StateMachine**。 可以在属性网格或直接在活动设计器的标头中编辑该值。 <xref:System.Activities.Activity.DisplayName%2A> 用于痕迹导航，后者显示在工作流设计器顶部。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|

## <a name="see-also"></a>请参阅

- [流程图](../workflow-designer/flowchart-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)