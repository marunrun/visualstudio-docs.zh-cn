---
title: 工作流设计器 CompensableActivity 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.CompensableActivity.UI
ms.assetid: e0340d89-d39e-4a52-8557-13e27040d7b5
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f498c6d025e7527b9767284a77c953e538cef377
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650667"
---
# <a name="compensableactivity-activity-designer"></a>CompensableActivity 活动设计器

" **CompensableActivity** " 活动设计器用于创建和配置 <xref:System.Activities.Statements.CompensableActivity> 活动。

## <a name="the-compensableactivity-activity"></a>CompensableActivity 活动
 <xref:System.Activities.Statements.CompensableActivity> 定义可在成功完成之后得到确认或补偿的工作单元。

### <a name="using-the-compensableactivity-activity-designer"></a>使用 CompensableActivity 活动设计器
 " **CompensableActivity** " 活动设计器可在 "**工具箱**" 的 "**事务**" 类别中找到。 若要打开**工具箱**，请选择工作流设计器左侧的 "**工具箱**" 选项卡。 或者，从 "**视图**" 菜单中选择 **"工具箱**"，或按**Ctrl** +**Alt** +**X**。

 可以将 " **CompensableActivity** " 活动设计器从 **"工具箱**" 拖放到工作流设计器图面上。 可以将活动设计器放在 <xref:System.Activities.Statements.Sequence> 中。 删除活动设计器将创建一个 <xref:System.Activities.Statements.CompensableActivity> 的活动，其默认 <xref:System.Activities.Activity.DisplayName%2A> 为 CompensableActivity。 编辑 " **CompensableActivity** " 活动设计器的标头中的 <xref:System.Activities.Activity.DisplayName%2A> 值。 它还可在属性网格的 " **DisplayName** " 框中进行编辑。

### <a name="the-compensableactivity-properties"></a>CompensableActivity 属性
 下表列出 <xref:System.Activities.Statements.CompensableActivity> 属性并说明如何在设计器中使用它们。 @No__t_0 和 <xref:System.Activities.Activity%601.Result%2A> 属性可以在属性网格中进行编辑，但其他属性必须在工作流设计器图面上进行编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.CompensableActivity> 活动的可选友好名称。 默认值为 CompensableActivity。|
|<xref:System.Activities.Activity%601.Result%2A>|False|指定 <xref:System.Activities.Statements.CompensableActivity> 的返回值。 此属性必须在属性网格中进行编辑。|
|<xref:System.Activities.Statements.CompensableActivity.Body%2A>|True|指定为其提供补偿、取消和确认逻辑的活动。 若要添加 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 活动，请将 **"工具箱**" 中的活动拖到 " **CompensableActivity** " 活动设计器上的 "**正文**" 框中。 添加提示文本 "在此处放置活动"。|
|<xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>|False|指定在取消时执行的活动。 若要添加活动，请将其设计器从 **"工具箱**" 拖到 " **CompensableActivity** " 活动设计器上的 " **CancellationHandler** " 框。 添加提示文本 "在此处放置活动"。|
|<xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>|False|指定补偿 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 活动时要执行的活动。 可使用 <xref:System.Activities.Statements.Compensate> 活动显式调用此处理程序。<br /><br /> 若要添加活动，请将其活动设计器从 **"工具箱**" 拖到 " **CompensableActivity** " 活动设计器上的 " **CompensationHandler** " 框中。 添加提示文本 "在此处放置活动"。|
|<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A>|False|指定确认 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 活动时要执行的活动。 可使用 <xref:System.Activities.Statements.Confirm> 活动显式调用此处理程序。<br /><br /> 若要添加活动，请将其活动设计器从 **"工具箱**" 拖到 " **CompensableActivity** " 活动设计器上的 " **ConfirmationHandler** " 框中。 添加提示文本 "在此处放置活动"。|

## <a name="see-also"></a>请参阅

- [事务](../workflow-designer/transaction-activity-designers.md)
- [CancellationScope](../workflow-designer/cancellationscope-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [Confirm](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)