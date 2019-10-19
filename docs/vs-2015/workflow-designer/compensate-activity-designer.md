---
title: 补偿活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Compensate.UI
ms.assetid: 7347c947-bfff-4bad-becd-5cd23e7b24cd
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 706cd446e931d6a3a065a3e8abfb58b5a90e9152
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656981"
---
# <a name="compensate-activity-designer"></a>Compensate 活动设计器
"**补偿**活动设计器" 用于创建和配置 <xref:System.Activities.Statements.Compensate> 活动。

## <a name="the-compensate-activity"></a>Compensate 活动
 <xref:System.Activities.Statements.Compensate> 活动为 <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> 中包含的活动显式调用 <xref:System.Activities.Statements.CompensableActivity>。 如果 <xref:System.Activities.Statements.Compensate> 活动未在 <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> 的 <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>、<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> 或 <xref:System.Activities.Statements.CompensableActivity> 中使用，则必须指定 <xref:System.Activities.Statements.Compensate.Target%2A> 属性。

 由 <xref:System.Activities.Statements.CompensationToken> 指定的 <xref:System.Activities.Statements.Compensate.Target%2A> 提供了在 <xref:System.Activities.Statements.CompensableActivity> 的 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 成功完成之后显式确认或补偿 <xref:System.Activities.Statements.CompensableActivity> 的方法。

### <a name="using-the-compensate-activity-designer"></a>使用 Compensate 活动设计器
 "**补偿**活动" 设计器可在 "**工具箱**" 的 "**事务**" 类别中找到，可通过单击 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 左侧的 "**工具箱**" 选项卡（或者 **，从** **"视图**" 菜单或 CTRL + ALT + X。）

 可以将 "**补偿**" 活动设计器从 "**工具箱**" 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence> 内。 这将创建具有 Compensate 的默认 <xref:System.Activities.Statements.Compensate> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 可以在 "**补偿**活动" 设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 值。

### <a name="the-compensate-properties"></a>Compensate 属性
 下表列出 <xref:System.Activities.Statements.CancellationScope> 属性并说明如何在设计器中使用它们。 <xref:System.Activities.Activity.DisplayName%2A> 属性可在属性网格中或 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上进行编辑，但 <xref:System.Activities.Statements.Compensate.Target%2A> 属性必须在属性网格中编辑。

|属性名|必需|用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.Compensate> 活动的可选友好名称。 默认值为 Compensate。|
|<xref:System.Activities.Statements.Compensate.Target%2A>|True|指定 <xref:System.Activities.InArgument%601>，它包含此 <xref:System.Activities.Statements.CompensationToken> 活动的 <xref:System.Activities.Statements.Compensate>。|

## <a name="see-also"></a>请参阅
 [Transaction](../workflow-designer/transaction-activity-designers.md) [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md) [补偿活动设计器](../workflow-designer/compensate-activity-designer.md)[确认](../workflow-designer/confirm-activity-designer.md) [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)