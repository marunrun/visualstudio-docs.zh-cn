---
title: ForEach &lt; T &gt; 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ForEach`1.UI
ms.assetid: 67097b3a-fcf5-4a72-beb1-2c7784151a86
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d41451ada0e37f953e9d611a4e3733815a9d347b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656654"
---
# <a name="foreachlttgt-activity-designer"></a>ForEach &lt; T &gt; 活动设计器
对于指定 <xref:System.Activities.Statements.ForEach%601> 集合中的每一项，<xref:System.Activities.Statements.ForEach%601.Body%2A> 活动执行包含在它的 <xref:System.Activities.Statements.ForEach%601.Values%2A> 中的活动。

## <a name="foreacht-properties-in-the-workflow-designer"></a>\<T>工作流设计器中的 ForEach 属性
 下表列出最有用的 <xref:System.Activities.Statements.ForEach%601> 活动属性并说明如何在设计器中使用它们。

|属性名称|必选|使用情况|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.ForEach%601> 活动的友好名称。 默认值为 ForEach \<Int32> 。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.ForEach%601.Values%2A>|正确|要循环访问的项的集合。 若要设置 <xref:System.Activities.Statements.ForEach%601.Values%2A> ，请 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 在 " **ForEach \<T> ** " 活动设计器或属性网格中的 "**值**" 框中键入表达式。|
|*TypeArgument*|正确|<xref:System.Activities.Statements.ForEach%601.Values%2A>由泛型参数*T*指定的集合中的项的类型。默认情况下， *TypeArgument*设置为**Int32**。 若要更改类型，请在属性网格中更改 " *TypeArgument* " 组合框的值。|

 默认情况下，循环迭代器为 " **项**"。 可在 <xref:System.Activities.Statements.ForEach%601> 活动设计器中更改迭代器变量的名称。 循环迭代器可在 <xref:System.Activities.Statements.ForEach%601> 活动的子级中的表达式中使用。

## <a name="see-also"></a>另请参阅
 [ParallelForEach \<T> ](../workflow-designer/parallelforeach-t-activity-designer.md)[控制流](../workflow-designer/control-flow-activity-designers.md)