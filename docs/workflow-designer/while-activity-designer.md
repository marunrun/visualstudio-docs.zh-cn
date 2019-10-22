---
title: 工作流设计器活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.While.UI
ms.assetid: ea008091-2e4c-4f64-bfa5-afb919552446
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6570a80de5be17b2893fc4105f057e655e841881
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72649769"
---
# <a name="while-activity-designer"></a>While 活动设计器

@No__t_0 活动执行其 <xref:System.Activities.Statements.While.Body%2A> 中包含的活动，而指定 <xref:System.Activities.Statements.While.Condition%2A> 的计算结果为**true**。 包含的活动可能永远都不会执行。 如果希望所包含的活动至少执行一次，请改用 <xref:System.Activities.Statements.DoWhile> 活动。

## <a name="while-properties-in-workflow-designer"></a>工作流设计器中的 While 属性

下表列出最有用的 <xref:System.Activities.Statements.While> 活动属性并说明如何在设计器中使用它们。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.While> 活动设计器在标头中的友好名称。 默认值为 While。 该值可以在 "**属性**" 窗口中编辑，也可以直接在活动设计器标头中编辑。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.While.Body%2A>|False|包含在 <xref:System.Activities.Statements.While.Condition%2A> 计算结果为**true**时要执行的活动。|
|<xref:System.Activities.Statements.While.Condition%2A>|True|包含计算以确定是否要执行 <xref:System.Activities.Statements.While.Body%2A> 中的活动的 Visual Basic 表达式。|

## <a name="see-also"></a>请参阅

- [控制流](../workflow-designer/control-flow-activity-designers.md)
- [DoWhile](../workflow-designer/dowhile-activity-designer.md)