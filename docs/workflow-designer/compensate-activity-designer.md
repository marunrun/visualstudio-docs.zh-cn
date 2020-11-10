---
title: 工作流设计器补偿活动设计器
description: 了解 "补偿活动设计器"，以及如何使用 "补偿活动设计器" 创建和配置补偿活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Compensate.UI
ms.assetid: 7347c947-bfff-4bad-becd-5cd23e7b24cd
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 96ae76bac3f6163e8b4434878017df07f1341828
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94434319"
---
# <a name="compensate-activity-designer"></a>Compensate 活动设计器

" **补偿** 活动设计器" 用于创建和配置 <xref:System.Activities.Statements.Compensate> 活动。

## <a name="the-compensate-activity"></a>Compensate 活动

<xref:System.Activities.Statements.Compensate> 活动为 <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> 中包含的活动显式调用 <xref:System.Activities.Statements.CompensableActivity>。 如果 <xref:System.Activities.Statements.Compensate> 活动未在 <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> 的 <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>、<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> 或 <xref:System.Activities.Statements.CompensableActivity> 中使用，则必须指定 <xref:System.Activities.Statements.Compensate.Target%2A> 属性。

由 <xref:System.Activities.Statements.CompensationToken> 指定的 <xref:System.Activities.Statements.Compensate.Target%2A> 提供了在 <xref:System.Activities.Statements.CompensableActivity> 的 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 成功完成之后显式确认或补偿 <xref:System.Activities.Statements.CompensableActivity> 的方法。

### <a name="using-the-compensate-activity-designer"></a>使用 Compensate 活动设计器

" **补偿** 活动" 设计器可在 " **工具箱** " 的 " **事务** " 类别中找到。 若要打开 **工具箱** ，请选择工作流设计器左侧的 " **工具箱** " 选项卡。 或者，从 " **视图** " 菜单中选择 **"工具箱** "，或按 **Ctrl** + **Alt** + **X** 。

可以将 " **补偿** 活动设计器" 从 " **工具箱** " 拖放到工作流设计器图面上放置活动的任何位置，如内 <xref:System.Activities.Statements.Sequence> 。 删除活动设计器将创建一个 <xref:System.Activities.Statements.Compensate> 活动，其中默认值为 " <xref:System.Activities.Activity.DisplayName%2A> 补偿"。 <xref:System.Activities.Activity.DisplayName%2A>可以在 " **补偿** 活动" 设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑值。

### <a name="the-compensate-properties"></a>Compensate 属性

下表列出 <xref:System.Activities.Statements.CancellationScope> 属性并说明如何在设计器中使用它们。 <xref:System.Activities.Activity.DisplayName%2A>属性可在属性网格中或工作流设计器图面上进行编辑。 <xref:System.Activities.Statements.Compensate.Target%2A>在属性网格中编辑属性。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.Compensate> 活动的可选友好名称。 默认值为 Compensate。|
|<xref:System.Activities.Statements.Compensate.Target%2A>|正确|指定 <xref:System.Activities.InArgument%601>，它包含此 <xref:System.Activities.Statements.CompensationToken> 活动的 <xref:System.Activities.Statements.Compensate>。|

## <a name="see-also"></a>另请参阅

- [事务](../workflow-designer/transaction-activity-designers.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensate 活动设计器](../workflow-designer/compensate-activity-designer.md)
- [逐条](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)