---
title: 工作流设计器-Assign 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Assign.UI
ms.assetid: ba3feb3c-f144-47ea-926d-cf752b804153
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4179c23cefbf995242288c1e778f9e0413bfe28e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993249"
---
# <a name="assign-activity-designer"></a>Assign 活动设计器

**分配**活动设计器用于创建和配置<xref:System.Activities.Statements.Assign>活动。

## <a name="the-assign-activity"></a>Assign 活动

<xref:System.Activities.Statements.Assign> 活动为变量或自变量赋值。

### <a name="using-the-assign-activity-designer"></a>使用 Assign 活动设计器

**分配**活动设计器可在**基元**的类别**工具箱**，这通过单击来访问**工具箱**选项卡 (或者，选择**工具箱**从**视图**菜单或 CTRL + ALT + X。)

**分配**活动设计器可以从拖动**工具箱**并在任何位置放置活动的如内放置到工作流设计器图面<xref:System.Activities.Statements.Sequence>。 删除**分配**活动设计器创建<xref:System.Activities.Statements.Assign>默认值的活动**DisplayName**的分配。 <xref:System.Activities.Activity.DisplayName%2A>可以在的标头中编辑**分配**活动设计器中或在**DisplayName**属性网格的框。

### <a name="the-assign-properties"></a>Assign 属性

下表列出 <xref:System.Activities.Statements.Assign> 属性并说明如何在设计器中使用它们。 可以在属性网格中编辑这些属性，其中一些可以在工作流设计器图面上进行编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.Assign> 活动的友好名称。 默认值为 Assign。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.Assign.To%2A>|True|为其赋 <xref:System.Activities.Statements.Assign.Value%2A> 的变量或自变量。 值必须是有效的 Visual Basic 标识符。 若要设置该属性，键入 Visual Basic 表达式**到**框**分配**活动设计器或在属性网格中。|
|<xref:System.Activities.Statements.Assign.Value%2A>|True|赋给变量的值。 若要设置<xref:System.Activities.Statements.Assign.Value%2A>，键入 Visual Basic 表达式**值**框**分配**活动设计器或在属性网格中。|

## <a name="see-also"></a>请参阅

- [基元](../workflow-designer/primitives-activity-designers.md)
- [Delay](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)