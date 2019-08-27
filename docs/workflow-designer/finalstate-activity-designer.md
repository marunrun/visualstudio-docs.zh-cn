---
title: 工作流设计器-FinalState 活动设计器
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: aa186893-8775-40dd-981f-8593ead831d0
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 8292e22bac6063a36286930584e1d7c227913511
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62949680"
---
# <a name="finalstate-activity-designer"></a>FinalState 活动设计器

<xref:System.Activities.Core.Presentation.FinalState> 设计器用于创建终止状态机实例的 <xref:System.Activities.Statements.State>。

## <a name="using-the-finalstate-activity-designer"></a>使用 FinalState 活动设计器

**FinalState**设计器用于创建<xref:System.Activities.Statements.State>预配置为终止状态机中的状态。 一个<xref:System.Activities.Statements.State>创建使用<xref:System.Activities.Core.Presentation.FinalState>活动设计器具有其<xref:System.Activities.Statements.State.IsFinal%2A>属性设置为**true**，没有<xref:System.Activities.Statements.State.Exit%2A>活动，并没有源自它的转换。 若要使用<xref:System.Activities.Core.Presentation.FinalState>活动设计器添加<xref:System.Activities.Statements.State>预配置为在状态机中的终止状态的活动拖动**FinalState**活动设计器从**状态机**一节**工具箱**拖放到工作流设计器。 <xref:System.Activities.Core.Presentation.FinalState> 活动设计器可以放置到 <xref:System.Activities.Statements.StateMachine> 上，以后可添加转换；或在删除 <xref:System.Activities.Core.Presentation.FinalState> 活动设计器时可创建转换。 创建转换的详细信息，请参阅[过渡](../workflow-designer/transition-activity-designer.md)。

### <a name="state-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 State 活动属性

下表列出可使用 <xref:System.Activities.Core.Presentation.FinalState> 设计器设置的属性并说明如何在设计器中使用它们。 其中一些属性可以在属性网格中进行编辑，另一些属性可以在设计器图面上进行编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Statements.State.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.State> 活动设计器在标头中的友好名称。 默认值是**状态**。 可以在属性网格或直接在活动设计器的标头中编辑该值。 <xref:System.Activities.Statements.State.DisplayName%2A> 用于痕迹导航，后者显示在工作流设计器顶部。<br /><br /> 虽然 <xref:System.Activities.Statements.State.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.State.Entry%2A>|False|指定在转换到此状态时发生的操作。 此值可以设置通过拖动将活动从**工具箱**并将其放置到<xref:System.Activities.Statements.State.Entry%2A>状态的部分。|

## <a name="see-also"></a>请参阅

- [StateMachine](../workflow-designer/statemachine-activity-designer.md)
- [状态](../workflow-designer/state-activity-designer.md)
- [Transition](../workflow-designer/transition-activity-designer.md)