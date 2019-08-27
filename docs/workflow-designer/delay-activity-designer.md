---
title: 工作流设计器-Delay 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Delay.UI
ms.assetid: f51742a8-2c9a-47d1-8a23-18459d03ae19
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e69c82899cb5f7aa24235641ae517709686170a7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62949755"
---
# <a name="delay-activity-designer"></a>Delay 活动设计器

**延迟**活动设计器用于创建和配置<xref:System.Activities.Statements.Delay>活动。

## <a name="the-delay-activity"></a>延迟活动

<xref:System.Activities.Statements.Delay> 活动可将工作流的执行延迟指定时长。

### <a name="use-the-delay-activity-designer"></a>使用 Delay 活动设计器

**延迟**活动设计器可在**基元**类别**工具箱**，这通过单击来访问**工具箱**工作流设计器选项卡。 或者，选择**工具箱**从**视图**菜单中或按**Ctrl**+**Alt** + **X**。

**延迟**活动设计器可以从拖动**工具箱**只要通常放置活动的例如内放置到工作流设计器图面和<xref:System.Activities.Statements.Sequence>。 放置在活动设计器创建<xref:System.Activities.Statements.Delay>默认值的活动<xref:System.Activities.Activity.DisplayName%2A>的延迟。 <xref:System.Activities.Activity.DisplayName%2A>可以在的标头中编辑**延迟**活动设计器中或在**DisplayName**属性网格的框。

### <a name="the-delay-properties"></a>延迟属性

下表显示<xref:System.Activities.Statements.Delay>属性并说明它们如何使用在设计器中。 可以在属性网格中编辑这些属性，其中一些可以在工作流设计器图面上进行编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.Delay> 活动的友好名称。 默认值为 Delay。 尽管<xref:System.Activities.Activity.DisplayName%2A>值并非是严格要求，它是使用其中一个是最佳做法。|
|<xref:System.Activities.Statements.Delay.Duration%2A>|True|将工作流延迟的时长。 此属性在属性网格中设置。 键入 00:00:00 格式的文本 <xref:System.TimeSpan> 或 Visual Basic 表达式来指定时长。|

## <a name="see-also"></a>请参阅

- [基元](../workflow-designer/primitives-activity-designers.md)
- [Assign](../workflow-designer/assign-activity-designer.md)
- [Delay 活动设计器](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)