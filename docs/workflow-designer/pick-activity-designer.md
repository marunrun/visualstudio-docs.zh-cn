---
title: 工作流设计器的 Pick 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Pick.UI
ms.assetid: 642c0a47-1b47-45de-a19a-ca0606cedd7a
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ed558c40e932f2148f2240247d19a4fc6df0d06a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63003586"
---
# <a name="pick-activity-designer"></a>Pick 活动设计器

<xref:System.Activities.Statements.Pick> 活动提供基于事件的控制流。 该活动执行多个分支中的一个分支来响应某个触发的事件。

## <a name="the-pick-activity"></a>Pick 活动

<xref:System.Activities.Statements.Pick> 活动包含一个 <xref:System.Activities.Statements.PickBranch> 对象的集合，<xref:System.Activities.Statements.Pick> 活动会由于某些作为触发器的传入事件而执行其中一个对象。 这种方式在工作流设计器提供了基于事件的控制流建模。 每个 <xref:System.Activities.Statements.PickBranch> 都包含一个 <xref:System.Activities.Statements.PickBranch.Trigger%2A> 和一个 <xref:System.Activities.Statements.PickBranch.Action%2A>。 在开头<xref:System.Activities.Statements.Pick>活动的执行，所有触发器活动<xref:System.Activities.Statements.PickBranch>计划元素。 在第一个活动完成之后，安排其相应的操作活动，并且取消所有其他触发器活动。

### <a name="how-to-use-the-pick-activity-designer"></a>如何使用 Pick 活动设计器

访问**选取**中的活动设计器**控制流**类别**工具箱**。 **选取**活动设计器可以从拖动**工具箱**无论通常放置活动设计器，有关示例，在何处放置到工作流设计器图面和**序列**活动设计器。 之后将它放到工作流设计器，它会创建<xref:System.Activities.Statements.Pick>活动，其中默认情况下包含两个空<xref:System.Activities.Statements.PickBranch>活动时，具有的元素显示为 Branch1 和 Branch2 的名称。 二者各自<xref:System.Activities.Statements.PickBranch.DisplayName%2A>属性值可以在中编辑**PickBranch**活动设计器标头中或在**属性**窗口为每个分支。

有两种方法来添加<xref:System.Activities.Statements.PickBranch>活动的集合<xref:System.Activities.Statements.Pick>对象： 拖放**PickBranch**从设计器**工具箱**或通过使用右键单击菜单从内部**选取**设计图面。 有关详细信息，请参阅[PickBranch](../workflow-designer/pickbranch-activity-designer.md)主题。 请注意的唯一项，可以放置在**选取**活动设计器是**PickBranch**活动设计器。

### <a name="pick-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 Pick 活动属性

下表列出 <xref:System.Activities.Statements.Pick> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.Pick> 活动设计器在标头中的友好名称。 默认值为 Pick。 可以在属性网格或直接在活动设计器的标头中编辑该值。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|

## <a name="see-also"></a>请参阅

- [控制流](../workflow-designer/control-flow-activity-designers.md)
- [Pick 活动](/dotnet/framework/windows-workflow-foundation/pick-activity)
- [使用 Pick 活动](/dotnet/framework/windows-workflow-foundation/samples/using-the-pick-activity)