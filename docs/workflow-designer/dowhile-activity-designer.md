---
title: 工作流设计器 DoWhile 活动设计器
description: 了解 "DoWhile" 活动如何执行其正文中包含的活动至少一次，直到指定条件的计算结果为 false。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.DoWhile.UI
ms.assetid: 948deb35-d72f-462b-bea6-4b119c10a148
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8385fe376f56738d76e066dc172e7b6b516f9a08
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94438056"
---
# <a name="dowhile-activity-designer"></a>DoWhile 活动设计器

<xref:System.Activities.Statements.DoWhile>活动将至少执行一次包含的活动 <xref:System.Activities.Statements.DoWhile.Body%2A> ，直到指定条件的计算结果为 **false** 。 如果需要执行循环体中包含的活动零次或多次，请改用 <xref:System.Activities.Statements.While> 活动。

## <a name="dowhile-properties-in-the-workflow-designer"></a>工作流设计器中的 DoWhile 属性

下表显示最有用的 <xref:System.Activities.Statements.DoWhile> 活动属性，并说明如何在设计器中使用它们：

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Statements.DoWhile.Body%2A>|错误|当条件为 **true** 时要执行的活动。 若要添加 <xref:System.Activities.Statements.DoWhile.Body%2A> 活动，请将活动从 "工具箱" 拖放到 " **DoWhile** " 活动设计器上的 " **正文** " 框中，其中包含提示文本 "将活动放在此处"。|
|<xref:System.Activities.Statements.DoWhile.Condition%2A>|正确|每次循环迭代后要计算的条件。 若要设置 <xref:System.Activities.Statements.DoWhile.Condition%2A> ，请在 " **DoWhile** " 活动设计器或属性网格中的 " **条件** " 框中键入 Visual Basic 表达式。|

## <a name="see-also"></a>另请参阅

- [While](../workflow-designer/while-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)