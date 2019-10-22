---
title: 工作流设计器延迟活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Delay.UI
ms.assetid: f51742a8-2c9a-47d1-8a23-18459d03ae19
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5190807bba08f05e176acc15ac8daf42ac028c50
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650550"
---
# <a name="delay-activity-designer"></a>Delay 活动设计器

"**延迟**" 活动设计器用于创建和配置 <xref:System.Activities.Statements.Delay> 活动。

## <a name="the-delay-activity"></a>延迟活动

<xref:System.Activities.Statements.Delay> 活动可将工作流的执行延迟指定时长。

### <a name="use-the-delay-activity-designer"></a>使用 Delay 活动设计器

"**延迟**" 活动设计器可在 "**工具箱**" 的 "**基元**" 类别中找到，可通过单击工作流设计器的 "**工具箱**" 选项卡进行访问。 或者，从 "**视图**" 菜单中选择 **"工具箱**"，或按**Ctrl** +**Alt** +**X**。

可以将 "**延迟**" 活动设计器从 "**工具箱**" 拖放到工作流设计器图面上通常放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence> 内。 删除活动设计器将创建一个 <xref:System.Activities.Statements.Delay> 的活动，该活动具有默认的延迟 <xref:System.Activities.Activity.DisplayName%2A>。 可以在 "**延迟**" 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A>。

### <a name="the-delay-properties"></a>延迟属性

下表显示 <xref:System.Activities.Statements.Delay> 属性，并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性可以在工作流设计器图面上进行编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.Delay> 活动的友好名称。 默认值为 Delay。 尽管不是严格要求 <xref:System.Activities.Activity.DisplayName%2A> 值，但最佳做法是使用一个。|
|<xref:System.Activities.Statements.Delay.Duration%2A>|True|将工作流延迟的时长。 此属性在属性网格中设置。 键入 00:00:00 格式的文本 <xref:System.TimeSpan> 或 Visual Basic 表达式来指定时长。|

## <a name="see-also"></a>请参阅

- [基元](../workflow-designer/primitives-activity-designers.md)
- [Assign](../workflow-designer/assign-activity-designer.md)
- [Delay 活动设计器](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)