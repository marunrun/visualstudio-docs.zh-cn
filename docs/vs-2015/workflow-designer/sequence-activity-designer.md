---
title: Sequence 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Sequence.UI
ms.assetid: 51c8d3cb-4d43-458f-9631-b63755f9ac94
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3acf02ab478eee244557e04f19f78ba2d5f0b950
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663262"
---
# <a name="sequence-activity-designer"></a>Sequence 活动设计器
<xref:System.Activities.Statements.Sequence> 活动包含子活动的已排序集合，将按该排序执行这些子活动。

 按顺序执行一组活动的另一个方法是使用 <xref:System.Activities.Statements.Flowchart> 活动。 当你有一个简单的分支或循环程序流需要为图示建模时，请考虑使用[流程图](../workflow-designer/flowchart-activity-designer.md)。

## <a name="using-the-sequence-activity-designer"></a>使用 Sequence 活动设计器
 若要添加 <xref:System.Activities.Statements.Sequence> 活动，请将 "**序列**" 活动设计器从 "**工具箱**" 拖放到 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 图面上。 若要向此 <xref:System.Activities.Statements.Sequence> 活动添加子活动，请将 "**工具箱**" 中的某些其他活动拖放到框中的三角形上，并在提示文本 "将活动放在此处"。

### <a name="sequence-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 Sequence 活动属性
 下表列出 <xref:System.Activities.Statements.Sequence> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。

|属性名|必需|用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.Sequence> 活动设计器在标头中的友好名称。 默认值为 Sequence。 可以在属性网格或直接在活动设计器的标头中编辑该值。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|

## <a name="see-also"></a>请参阅
 [流程图](../workflow-designer/flowchart-activity-designer.md)[控制流](../workflow-designer/control-flow-activity-designers.md)