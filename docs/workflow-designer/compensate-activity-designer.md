---
title: 工作流设计器-Compensate 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Compensate.UI
ms.assetid: 7347c947-bfff-4bad-becd-5cd23e7b24cd
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c55ecd8e3402d927b11cc00d18d6d134a5b25681
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62949833"
---
# <a name="compensate-activity-designer"></a>Compensate 活动设计器

**Compensate**活动设计器用于创建和配置<xref:System.Activities.Statements.Compensate>活动。

## <a name="the-compensate-activity"></a>Compensate 活动

<xref:System.Activities.Statements.Compensate> 活动为 <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> 中包含的活动显式调用 <xref:System.Activities.Statements.CompensableActivity>。 如果 <xref:System.Activities.Statements.Compensate> 活动未在 <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> 的 <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>、<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> 或 <xref:System.Activities.Statements.CompensableActivity> 中使用，则必须指定 <xref:System.Activities.Statements.Compensate.Target%2A> 属性。

由 <xref:System.Activities.Statements.CompensationToken> 指定的 <xref:System.Activities.Statements.Compensate.Target%2A> 提供了在 <xref:System.Activities.Statements.CompensableActivity> 的 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 成功完成之后显式确认或补偿 <xref:System.Activities.Statements.CompensableActivity> 的方法。

### <a name="using-the-compensate-activity-designer"></a>使用 Compensate 活动设计器

**Compensate**活动设计器可在**事务**类别**工具箱**。 若要打开**工具箱**，选择**工具箱**左侧和右侧的工作流设计器上的选项卡。 或者，选择**工具箱**从**视图**菜单中或按**Ctrl**+**Alt** + **X**。

**Compensate**活动设计器可以从拖动**工具箱**无论在何处放置活动的如内放置到工作流设计器图面和<xref:System.Activities.Statements.Sequence>。 放置在活动设计器创建<xref:System.Activities.Statements.Compensate>默认值的活动<xref:System.Activities.Activity.DisplayName%2A>的补偿。 <xref:System.Activities.Activity.DisplayName%2A>值可以在的标头中编辑**补偿**活动设计器中或在**DisplayName**属性网格的框。

### <a name="the-compensate-properties"></a>Compensate 属性

下表列出 <xref:System.Activities.Statements.CancellationScope> 属性并说明如何在设计器中使用它们。 <xref:System.Activities.Activity.DisplayName%2A>属性可以在属性网格中或在工作流设计器图面上进行编辑。 编辑<xref:System.Activities.Statements.Compensate.Target%2A>属性网格中的属性。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.Compensate> 活动的可选友好名称。 默认值为 Compensate。|
|<xref:System.Activities.Statements.Compensate.Target%2A>|True|指定 <xref:System.Activities.InArgument%601>，它包含此 <xref:System.Activities.Statements.CompensationToken> 活动的 <xref:System.Activities.Statements.Compensate>。|

## <a name="see-also"></a>请参阅

- [事务](../workflow-designer/transaction-activity-designers.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensate 活动设计器](../workflow-designer/compensate-activity-designer.md)
- [Confirm](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)