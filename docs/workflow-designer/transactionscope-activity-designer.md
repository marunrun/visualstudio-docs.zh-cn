---
title: 工作流设计器-TransactionScope 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.TransactionScope.UI
ms.assetid: 8d7ebfc6-7478-4888-b3b0-b14f296096af
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e84312518c19ef2a041091c5e2439dd7fb312c69
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62433963"
---
# <a name="transactionscope-activity-designer"></a>TransactionScope 活动设计器

**TransactionScope**活动设计器用于创建和配置<xref:System.Activities.Statements.TransactionScope>活动。

## <a name="the-transactionscope-activity"></a>TransactionScope 活动

<xref:System.Activities.Statements.TransactionScope> 活动在单个事务中执行所包含的活动。 在 <xref:System.Activities.Statements.TransactionScope.Body%2A> 活动以及该事务中的所有其他参与者成功完成时将提交该事务。

### <a name="using-the-transactionscope-activity-designer"></a>使用 TransactionScope 活动设计器

访问**TransactionScope**中的活动设计器**事务**类别**工具箱**。 **TransactionScope**活动设计器可以从拖动**工具箱**只要通常放置活动的例如内放置到工作流设计器图面和<xref:System.Activities.Statements.Sequence>。 这将创建具有 TransactionScope 的默认 <xref:System.Activities.Statements.TransactionScope> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 <xref:System.Activities.Activity.DisplayName%2A>值可以在的标头中编辑**TransactionScope**活动设计器中或在**DisplayName**属性网格的框。

### <a name="the-transactionscope-properties"></a>TransactionScope 属性

下表列出 <xref:System.Activities.Statements.TransactionScope> 属性并说明如何在设计器中使用它们。 <xref:System.Activities.Activity.DisplayName%2A>和<xref:System.Activities.Statements.TransactionScope.Body%2A>属性可以在工作流设计器图面上编辑。 但其他属性必须在属性网格上编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.TransactionScope> 活动的可选友好名称。 默认值为 TransactionScope。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.TransactionScope.Body%2A>|True|指定要在单个事务中执行的活动。 若要添加<xref:System.Activities.Statements.TransactionScope.Body%2A>活动，请将活动从拖**工具箱**到**正文**框**TransactionScope**带提示文本"放置活动的活动设计器在此处"。|
|<xref:System.Activities.Statements.TransactionScope.IsolationLevel%2A>|True|指定此 <xref:System.Transactions.IsolationLevel> 的 <xref:System.Activities.Statements.TransactionScope>。|
|<xref:System.Activities.Statements.TransactionScope.Timeout%2A>|False|指定必须在其间完成事务的时间间隔（格式为 00:00:00，表示小时:分钟:秒）。 默认值为 1 分钟 (00:01:00)。|
|[System.Activities.Statements.TransactionScope.AbortInstanceOnTransactionFailure](https://msdn.microsoft.com/library/system.activities.statements.transactionscope.abortinstanceontransactionfailure.aspx)|True|指定指示在事务中止的情况下是否应中止工作流的值。|

## <a name="see-also"></a>请参阅

- [事务](../workflow-designer/transaction-activity-designers.md)
- [TerminateWorkflow](../workflow-designer/terminateworkflow-activity-designer.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [Confirm](../workflow-designer/confirm-activity-designer.md)