---
title: While 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.While.UI
ms.assetid: ea008091-2e4c-4f64-bfa5-afb919552446
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 36752df3d8ffbf33b8ea95570d6a4efe8c8cd3be
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855400"
---
# <a name="while-activity-designer"></a>While 活动设计器

<xref:System.Activities.Statements.While>活动在执行中包含的活动及其<xref:System.Activities.Statements.While.Body%2A>时指定的条件计算结果为**true**。 包含的活动可能永远都不会执行。 如果希望所包含的活动至少执行一次，请改用 <xref:System.Activities.Statements.DoWhile> 活动。

## <a name="while-properties-in-workflow-designer"></a>工作流设计器中的 While 属性

下表列出最有用的 <xref:System.Activities.Statements.While> 活动属性并说明如何在设计器中使用它们。

|属性名|必需|用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.While> 活动设计器在标头中的友好名称。 默认值为 While。 可以在编辑该值**属性**窗口或直接在活动设计器标头。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.While.Body%2A>|False|包含要执行的活动时<xref:System.Activities.Statements.While.Condition%2A>计算结果为**true**。|
|<xref:System.Activities.Statements.While.Condition%2A>|True|包含 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 表达式，通过计算该表达式来确定是否要执行 <xref:System.Activities.Statements.While.Body%2A> 中的活动。|

## <a name="see-also"></a>请参阅

- [控制流](../workflow-designer/control-flow-activity-designers.md)
- [DoWhile](../workflow-designer/dowhile-activity-designer.md)