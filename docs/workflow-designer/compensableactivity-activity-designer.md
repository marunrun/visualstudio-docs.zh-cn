---
title: 工作流设计器-CompensableActivity 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.CompensableActivity.UI
ms.assetid: e0340d89-d39e-4a52-8557-13e27040d7b5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cfe5a207136b44e61beff77bec8c8c7b869568b6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62949886"
---
# <a name="compensableactivity-activity-designer"></a>CompensableActivity 活动设计器

**CompensableActivity**活动设计器用于创建和配置<xref:System.Activities.Statements.CompensableActivity>活动。

## <a name="the-compensableactivity-activity"></a>CompensableActivity 活动
 <xref:System.Activities.Statements.CompensableActivity> 定义可在成功完成之后得到确认或补偿的工作单元。

### <a name="using-the-compensableactivity-activity-designer"></a>使用 CompensableActivity 活动设计器
 **CompensableActivity**活动设计器可在**事务**类别**工具箱**。 若要打开**工具箱**，选择**工具箱**左侧和右侧的工作流设计器上的选项卡。 或者，选择**工具箱**从**视图**菜单中或按**Ctrl**+**Alt** + **X**。

 **CompensableActivity**活动设计器可以从拖动**工具箱**和放置到工作流设计器图面。 无法删除活动设计器内的<xref:System.Activities.Statements.Sequence>。 放置在活动设计器创建<xref:System.Activities.Statements.CompensableActivity>默认值的活动<xref:System.Activities.Activity.DisplayName%2A>的 CompensableActivity。 编辑<xref:System.Activities.Activity.DisplayName%2A>的标头的值**CompensableActivity**活动设计器。 此外可以在中编辑**DisplayName**属性网格的框。

### <a name="the-compensableactivity-properties"></a>CompensableActivity 属性
 下表列出 <xref:System.Activities.Statements.CompensableActivity> 属性并说明如何在设计器中使用它们。 <xref:System.Activities.Activity.DisplayName%2A>和<xref:System.Activities.Activity%601.Result%2A>属性可以在属性网格中编辑，但其他属性必须编辑工作流设计器图面上。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.CompensableActivity> 活动的可选友好名称。 默认值为 CompensableActivity。|
|<xref:System.Activities.Activity%601.Result%2A>|False|指定 <xref:System.Activities.Statements.CompensableActivity> 的返回值。 此属性必须在属性网格中进行编辑。|
|<xref:System.Activities.Statements.CompensableActivity.Body%2A>|True|指定为其提供补偿、取消和确认逻辑的活动。 若要添加<xref:System.Activities.Statements.CompensableActivity.Body%2A>活动，请将活动从拖**工具箱**到**正文**框**CompensableActivity**活动设计器。 添加提示文本"此处放置活动"。|
|<xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>|False|指定取消时执行的活动。 若要添加活动，删除其设计器从**工具箱**成**CancellationHandler**框**CompensableActivity**活动设计器。 添加提示文本"此处放置活动"。|
|<xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>|False|指定补偿 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 活动时要执行的活动。 可使用 <xref:System.Activities.Statements.Compensate> 活动显式调用此处理程序。<br /><br /> 若要添加活动，删除其活动设计器从**工具箱**成**CompensationHandler**框**CompensableActivity**活动设计器。 添加提示文本"此处放置活动"。|
|<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A>|False|指定确认 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 活动时要执行的活动。 可使用 <xref:System.Activities.Statements.Confirm> 活动显式调用此处理程序。<br /><br /> 若要添加活动，删除其活动设计器从**工具箱**成**ConfirmationHandler**框**CompensableActivity**活动设计器。 添加提示文本"此处放置活动"。|

## <a name="see-also"></a>请参阅

- [事务](../workflow-designer/transaction-activity-designers.md)
- [CancellationScope](../workflow-designer/cancellationscope-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [Confirm](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)