---
title: 工作流设计器-确认活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Confirm.UI
ms.assetid: c753b67b-b0e7-462a-bb4e-ba8db04a078d
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cd17f71ff9e408c48493dc862dfe94f8d7037903
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650634"
---
# <a name="confirm-activity-designer"></a>Confirm 活动设计器

"**确认**" 活动设计器用于创建和配置 <xref:System.Activities.Statements.Confirm> 活动。

## <a name="the-confirm-activity"></a>Confirm 活动
 <xref:System.Activities.Statements.Confirm> 活动为 <xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> 中包含的活动显式调用 <xref:System.Activities.Statements.CompensableActivity>。 如果 <xref:System.Activities.Statements.Confirm> 活动未在 <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> 的 <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>、<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> 或 <xref:System.Activities.Statements.CompensableActivity> 中使用，则必须指定 <xref:System.Activities.Statements.Confirm.Target%2A> 属性。

 由 <xref:System.Activities.Statements.CompensationToken> 指定的 <xref:System.Activities.Statements.Compensate.Target%2A> 提供了在 <xref:System.Activities.Statements.CompensableActivity> 的 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 成功完成之后显式确认或补偿 <xref:System.Activities.Statements.CompensableActivity> 的方法。

### <a name="using-the-confirm-activity-designer"></a>使用 Confirm 活动设计器
 "**确认**" 活动设计器可在 "**工具箱**" 的 "**事务**" 类别中找到，可通过单击工作流设计器左侧的 "**工具箱**" 选项卡进行访问。 或者，从 "**视图**" 菜单中选择 **"工具箱**"，或按**Ctrl** +**Alt** +**X**。

 可以将 "**确认**" 活动设计器从 "**工具箱**" 拖放到工作流设计器图面上通常放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence> 内。 这将创建具有 Confirm 的默认 <xref:System.Activities.Statements.Confirm> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 可以在 "**确认**" 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 值。

### <a name="the-confirm-properties"></a>Confirm 属性
 下表列出 <xref:System.Activities.Statements.Confirm> 属性并说明如何在设计器中使用它们。 @No__t_0 属性可在属性网格中或工作流设计器图面上进行编辑，但 <xref:System.Activities.Statements.Confirm.Target%2A> 属性必须在属性网格中进行编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.CancellationScope> 活动的可选友好名称。 默认值为 Confirm。|
|<xref:System.Activities.Statements.Confirm.Target%2A>|True|指定 <xref:System.Activities.InArgument%601>，它包含此 <xref:System.Activities.Statements.CompensationToken> 活动的 <xref:System.Activities.Statements.Confirm>。|

## <a name="see-also"></a>请参阅

- [事务](../workflow-designer/transaction-activity-designers.md)
- [CancellationScope](../workflow-designer/cancellationscope-activity-designer.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)