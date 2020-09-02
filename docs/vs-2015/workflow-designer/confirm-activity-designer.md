---
title: 确认活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Confirm.UI
ms.assetid: c753b67b-b0e7-462a-bb4e-ba8db04a078d
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b3835c6cb537e7ac74862ac4a6794dd7b0bd5003
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656963"
---
# <a name="confirm-activity-designer"></a>Confirm 活动设计器
" **确认** " 活动设计器用于创建和配置 <xref:System.Activities.Statements.Confirm> 活动。

## <a name="the-confirm-activity"></a>Confirm 活动
 <xref:System.Activities.Statements.Confirm> 活动为 <xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> 中包含的活动显式调用 <xref:System.Activities.Statements.CompensableActivity>。 如果 <xref:System.Activities.Statements.Confirm> 活动未在 <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> 的 <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>、<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> 或 <xref:System.Activities.Statements.CompensableActivity> 中使用，则必须指定 <xref:System.Activities.Statements.Confirm.Target%2A> 属性。

 由 <xref:System.Activities.Statements.CompensationToken> 指定的 <xref:System.Activities.Statements.Compensate.Target%2A> 提供了在 <xref:System.Activities.Statements.CompensableActivity> 的 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 成功完成之后显式确认或补偿 <xref:System.Activities.Statements.CompensableActivity> 的方法。

### <a name="using-the-confirm-activity-designer"></a>使用 Confirm 活动设计器
 "**确认**" 活动设计器可在 "**工具箱**" 的 "**事务**" 类别中找到，可通过单击 (左侧的 "**工具箱**" 选项卡访问，也可以 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 从 "**视图**" 菜单中选择 "**工具栏**" 或按 CTRL + ALT + X。 ) 

 可以将 " **确认** " 活动设计器从 " **工具箱** " 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置，例如中 <xref:System.Activities.Statements.Sequence> 。 这将创建具有 Confirm 的默认 <xref:System.Activities.Statements.Confirm> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 <xref:System.Activities.Activity.DisplayName%2A>该值可以在 "**确认**" 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑。

### <a name="the-confirm-properties"></a>Confirm 属性
 下表列出 <xref:System.Activities.Statements.Confirm> 属性并说明如何在设计器中使用它们。 <xref:System.Activities.Activity.DisplayName%2A> 属性可在属性网格中或 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上进行编辑，但 <xref:System.Activities.Statements.Confirm.Target%2A> 属性必须在属性网格中编辑。

|属性名称|必选|使用情况|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.CancellationScope> 活动的可选友好名称。 默认值为 Confirm。|
|<xref:System.Activities.Statements.Confirm.Target%2A>|正确|指定 <xref:System.Activities.InArgument%601>，它包含此 <xref:System.Activities.Statements.CompensationToken> 活动的 <xref:System.Activities.Statements.Confirm>。|

## <a name="see-also"></a>另请参阅
 [Transaction](../workflow-designer/transaction-activity-designers.md) [CancellationScope](../workflow-designer/cancellationscope-activity-designer.md) [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md) [补偿](../workflow-designer/compensate-activity-designer.md) [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)