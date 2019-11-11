---
title: DoWhile 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.DoWhile.UI
ms.assetid: 948deb35-d72f-462b-bea6-4b119c10a148
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b63c3e2e0907bcaf13ada4cbb20ce5527a240fe3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656772"
---
# <a name="dowhile-activity-designer"></a>DoWhile 活动设计器
@No__t_0 活动将至少执行其 <xref:System.Activities.Statements.DoWhile.Body%2A> 中包含的活动，直到指定条件的计算结果为**false**。 如果需要执行循环体中包含的活动零次或多次，请改用 <xref:System.Activities.Statements.While> 活动。

## <a name="dowhile-properties-in-the-workflow-designer"></a>工作流设计器中的 DoWhile 属性
 下表列出最有用的 <xref:System.Activities.Statements.DoWhile> 活动属性并说明如何在设计器中使用它们。

|属性名|必需|用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Statements.DoWhile.Body%2A>|False|当条件为**true**时要执行的活动。 若要添加 <xref:System.Activities.Statements.DoWhile.Body%2A> 活动，请将活动从 "工具箱" 拖放到 " **DoWhile** " 活动设计器上的 "**正文**" 框中，其中包含提示文本 "将活动放在此处"。|
|<xref:System.Activities.Statements.DoWhile.Condition%2A>|True|每次循环迭代后要计算的条件。 若要设置 <xref:System.Activities.Statements.DoWhile.Condition%2A>，请在 " **DoWhile** " 活动设计器或属性网格中的 "**条件**" 框中键入 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 表达式。|

## <a name="see-also"></a>请参阅
 [While](../workflow-designer/while-activity-designer.md) [控制流](../workflow-designer/control-flow-activity-designers.md)