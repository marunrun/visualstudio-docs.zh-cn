---
title: 工作流设计器-Pick 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Pick.UI
ms.assetid: 642c0a47-1b47-45de-a19a-ca0606cedd7a
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 01ebd0dbfa8274b370a7e84b1033465e2be0b4a9
ms.sourcegitcommit: 186c0c250d85ac74274fa1e438b4c7c7108d8a36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86876029"
---
# <a name="pick-activity-designer"></a>Pick 活动设计器

<xref:System.Activities.Statements.Pick> 活动提供基于事件的控制流。 该活动执行多个分支中的一个分支来响应某个触发的事件。

## <a name="the-pick-activity"></a>Pick 活动

<xref:System.Activities.Statements.Pick> 活动包含一个 <xref:System.Activities.Statements.PickBranch> 对象的集合，<xref:System.Activities.Statements.Pick> 活动会由于某些作为触发器的传入事件而执行其中一个对象。 这样工作流设计器提供基于事件的控制流建模。 每个 <xref:System.Activities.Statements.PickBranch> 都包含一个 <xref:System.Activities.Statements.PickBranch.Trigger%2A> 和一个 <xref:System.Activities.Statements.PickBranch.Action%2A>。 在活动执行开始时 <xref:System.Activities.Statements.Pick> ，将安排元素的所有触发器活动 <xref:System.Activities.Statements.PickBranch> 。 在第一个活动完成之后，安排其相应的操作活动，并且取消所有其他触发器活动。

### <a name="how-to-use-the-pick-activity-designer"></a>如何使用 Pick 活动设计器

访问 "**工具箱**" 的 "**控制流**" 类别中的 " **Pick** " 活动设计器。 可以将 " **Pick** " 活动设计器从 "**工具箱**" 拖放到工作流设计器图面上通常放置活动设计器的任何位置，例如，在 " **Sequence** " 活动设计器内。 将其放入工作流设计器后，它将创建一个 <xref:System.Activities.Statements.Pick> 活动，该活动默认情况下包含两个空 <xref:System.Activities.Statements.PickBranch> 活动，作为显示名称为 Branch1 和 Branch2 的元素。 <xref:System.Activities.Statements.PickBranch.DisplayName%2A>可以在 " **PickBranch** " 活动设计器标头或每个分支的 "**属性**" 窗口中编辑这些各自的属性值。

可以通过两种方法将 <xref:System.Activities.Statements.PickBranch> 活动添加到对象的集合中 <xref:System.Activities.Statements.Pick> ：从 "**工具箱**" 拖放 " **PickBranch** " 设计器，或者使用 " **Pick** " 设计图面中的右键单击菜单。 有关详细信息，请参阅[PickBranch](../workflow-designer/pickbranch-activity-designer.md)主题。 请注意，可以放置在 " **Pick** " 活动设计器中的唯一项是 " **PickBranch** " 活动设计器。

### <a name="pick-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 Pick 活动属性

下表列出 <xref:System.Activities.Statements.Pick> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.Pick> 活动设计器在标头中的友好名称。 默认值为 Pick。 可以在属性网格或直接在活动设计器的标头中编辑该值。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|

## <a name="see-also"></a>另请参阅

- [控制流](../workflow-designer/control-flow-activity-designers.md)
- [Pick 活动](/dotnet/framework/windows-workflow-foundation/pick-activity)
- [使用 Pick 活动](/dotnet/framework/windows-workflow-foundation/samples/using-the-pick-activity)