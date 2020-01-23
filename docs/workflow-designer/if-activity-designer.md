---
title: 工作流设计器-If 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.If.UI
ms.assetid: 930a8fa2-db98-43e9-ad6d-a85cc7a6519a
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 099be38c5585fe19c00b31c00ac3a7ddcd3d7fe2
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76111465"
---
# <a name="if-activity-designer"></a>If 活动设计器

<xref:System.Activities.Statements.If> 活动计算条件并根据该计算结果执行活动。 当使用编程的过程建模样式时，此活动最有用。 例如，<xref:System.Activities.Statements.If> 活动可嵌套在 <xref:System.Activities.Statements.Sequence> 活动或 <xref:System.Activities.Statements.Parallel> 活动内。 如果您使用的是 <xref:System.Activities.Statements.Flowchart> 活动，请考虑改用 <xref:System.Activities.Statements.FlowDecision> 活动。

## <a name="if-properties-in-the-workflow-designer"></a>工作流设计器中的 If 属性

下表列出最有用的 <xref:System.Activities.Statements.If> 活动属性并说明如何在设计器中使用它们。

|属性名|必需|用量|
|-|--------------|-|
|<xref:System.Activities.Statements.If.Condition%2A>|True|用于确定要执行哪个子活动的条件。 若要设置 <xref:System.Activities.Statements.If.Condition%2A>，请在 " **If** " 活动设计器或属性网格中的 "**条件**" 框中键入 Visual Basic 表达式。|
|<xref:System.Activities.Statements.If.Else%2A>|False|<xref:System.Activities.Statements.If.Condition%2A> 为**false**时要执行的活动。 若要添加 <xref:System.Activities.Statements.If.Else%2A> 分支执行的活动，请将活动从 "**工具箱**" 拖放到 " **If** " 活动设计器上带提示文本 "将活动放置到此处" 的 " **Else** " 框中。|
|<xref:System.Activities.Statements.If.Then%2A>|False|<xref:System.Activities.Statements.If.Condition%2A> 为**true**时要执行的活动。 若要添加由 <xref:System.Activities.Statements.If.Then%2A> 分支执行的活动，请将活动从 "**工具箱**" 拖放到 " **If** " 活动设计器上的 "Then" 框，并提示文本 "**将**活动放在此处"。|

## <a name="see-also"></a>另请参阅

- [Sequence](../workflow-designer/sequence-activity-designer.md)
- [Parallel](../workflow-designer/parallel-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)
