---
title: CompensableActivity 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.CompensableActivity.UI
ms.assetid: e0340d89-d39e-4a52-8557-13e27040d7b5
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e2bc28c4586912d7c253c9629c2af0eefd30e47e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656996"
---
# <a name="compensableactivity-activity-designer"></a>CompensableActivity 活动设计器
" **CompensableActivity** " 活动设计器用于创建和配置 <xref:System.Activities.Statements.CompensableActivity> 活动。

## <a name="the-compensableactivity-activity"></a>CompensableActivity 活动
 <xref:System.Activities.Statements.CompensableActivity> 定义可在成功完成之后得到确认或补偿的工作单元。

### <a name="using-the-compensableactivity-activity-designer"></a>使用 CompensableActivity 活动设计器
 " **CompensableActivity** " 活动设计器可在 "**工具箱**" 的 "**事务**" 类别中找到，可通过单击 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 左侧的 "**工具箱**" 选项卡进行访问（或者选择**工具栏**从 "**视图**" 菜单或 CTRL + ALT + X。）

 可以将 " **CompensableActivity** " 活动设计器从 "**工具箱**" 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence> 内。 这将创建具有 CompensableActivity 的默认 <xref:System.Activities.Statements.CompensableActivity> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 可以在 " **CompensableActivity** " 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 值。

### <a name="the-compensableactivity-properties"></a>CompensableActivity 属性
 下表列出 <xref:System.Activities.Statements.CompensableActivity> 属性并说明如何在设计器中使用它们。 <xref:System.Activities.Activity.DisplayName%2A> 和 <xref:System.Activities.Activity%601.Result%2A> 属性可在属性网格中进行编辑，但其他属性必须在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上进行编辑。

|属性名|必需|用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.CompensableActivity> 活动的可选友好名称。 默认值为 CompensableActivity。|
|<xref:System.Activities.Activity%601.Result%2A>|False|指定 <xref:System.Activities.Statements.CompensableActivity> 的返回值。 此属性必须在属性网格中进行编辑。|
|<xref:System.Activities.Statements.CompensableActivity.Body%2A>|True|指定为其提供补偿、取消和确认逻辑的活动。 若要添加 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 活动，请将活动从 "**工具箱**" 拖放到 " **CompensableActivity** " 活动设计器上的 "**正文**" 框中，其中包含提示文本 "将活动放在此处"。|
|<xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>|False|指定在取消事件中执行的活动。 若要添加活动，请将 "工具箱" 中的设计器从 "**工具箱**" 拖放到 " **CompensableActivity** " 活动设计器上的 " **CancellationHandler** " 框中，并在提示文本 "drop|
|<xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>|False|指定补偿 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 活动时要执行的活动。 可使用 <xref:System.Activities.Statements.Compensate> 活动显式调用此处理程序。<br /><br /> 若要添加活动，请将其活动设计器从 "**工具箱**" 拖放到 " **CompensableActivity** " 活动设计器上的 " **CompensationHandler** " 框中，其中包含提示文本 "将活动拖放"|
|<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A>|False|指定确认 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 活动时要执行的活动。 可使用 <xref:System.Activities.Statements.Confirm> 活动显式调用此处理程序。<br /><br /> 若要添加活动，请将其活动设计器从 "**工具箱**" 拖放到 " **CompensableActivity** " 活动设计器上的 " **ConfirmationHandler** " 框中，其中包含提示文本 "将活动拖放"|

## <a name="see-also"></a>请参阅
 [Transaction](../workflow-designer/transaction-activity-designers.md) [CancellationScope](../workflow-designer/cancellationscope-activity-designer.md) [补偿](../workflow-designer/compensate-activity-designer.md)[确认](../workflow-designer/confirm-activity-designer.md) [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)