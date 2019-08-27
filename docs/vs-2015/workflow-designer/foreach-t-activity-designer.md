---
title: ForEach&lt;T&gt;活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ForEach`1.UI
ms.assetid: 67097b3a-fcf5-4a72-beb1-2c7784151a86
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 97732b92c5a90334917ad4e74667f88d605b647d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62943285"
---
# <a name="foreachlttgt-activity-designer"></a>ForEach&lt;T&gt;活动设计器
对于指定 <xref:System.Activities.Statements.ForEach%601> 集合中的每一项，<xref:System.Activities.Statements.ForEach%601.Body%2A> 活动执行包含在它的 <xref:System.Activities.Statements.ForEach%601.Values%2A> 中的活动。  
  
## <a name="foreacht-properties-in-the-workflow-designer"></a>ForEach\<T > 中的工作流设计器的属性  
 下表列出最有用的 <xref:System.Activities.Statements.ForEach%601> 活动属性并说明如何在设计器中使用它们。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.ForEach%601> 活动的友好名称。 默认值为 ForEach\<Int32 >。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|  
|<xref:System.Activities.Statements.ForEach%601.Values%2A>|True|要循环访问的项的集合。 若要设置<xref:System.Activities.Statements.ForEach%601.Values%2A>，键入[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]中的表达式**值**框**ForEach\<T >** 活动设计器或在属性网格中。|  
|*TypeArgument*|True|中的项的类型<xref:System.Activities.Statements.ForEach%601.Values%2A>由泛型参数指定的集合*T*。默认情况下*TypeArgument*设置为**Int32**。 若要更改的类型，更改的值*TypeArgument*属性网格中的组合框。|  
  
 默认情况下，循环迭代器称为**项**。 可在 <xref:System.Activities.Statements.ForEach%601> 活动设计器中更改迭代器变量的名称。 循环迭代器可在 <xref:System.Activities.Statements.ForEach%601> 活动的子级中的表达式中使用。  
  
## <a name="see-also"></a>请参阅  
 [ParallelForEach\<T>](../workflow-designer/parallelforeach-t-activity-designer.md)   
 [控制流](../workflow-designer/control-flow-activity-designers.md)