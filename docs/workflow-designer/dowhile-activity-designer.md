---
title: 工作流设计器-DoWhile 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.DoWhile.UI
ms.assetid: 948deb35-d72f-462b-bea6-4b119c10a148
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a0069d352897d2d98288988d549d9733a39b2c35
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62949729"
---
# <a name="dowhile-activity-designer"></a>DoWhile 活动设计器

<xref:System.Activities.Statements.DoWhile>活动在执行中包含的活动及其<xref:System.Activities.Statements.DoWhile.Body%2A>至少一次，直到指定的条件的计算结果为**false**。 如果需要执行循环体中包含的活动零次或多次，请改用 <xref:System.Activities.Statements.While> 活动。

## <a name="dowhile-properties-in-the-workflow-designer"></a>工作流设计器中的 DoWhile 属性

下表列出最有用<xref:System.Activities.Statements.DoWhile>活动属性，并介绍了如何在设计器中使用它们：

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Statements.DoWhile.Body%2A>|False|要执行该条件时的活动 **，则返回 true**。 若要添加<xref:System.Activities.Statements.DoWhile.Body%2A>活动，将活动从工具箱拖到拖**正文**框**DoWhile**带提示文本"此处放置活动"的活动设计器。|
|<xref:System.Activities.Statements.DoWhile.Condition%2A>|True|每次循环迭代后要计算的条件。 若要设置<xref:System.Activities.Statements.DoWhile.Condition%2A>，键入 Visual Basic 表达式**条件**框**DoWhile**活动设计器或在属性网格中。|

## <a name="see-also"></a>请参阅

- [While](../workflow-designer/while-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)