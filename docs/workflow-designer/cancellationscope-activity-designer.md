---
title: 工作流设计器 CancellationScope 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.CancellationScope.UI
ms.assetid: 2c85d663-b219-4142-9866-7693ffd46379
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a6d1067b529dffec5a4e6a1f21d5489c32311c07
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "76112505"
---
# <a name="cancellationscope-activity-designer"></a>CancellationScope 活动设计器

" **CancellationScope** " 活动设计器用于创建和配置 <xref:System.Activities.Statements.CancellationScope> 活动。

## <a name="the-cancellationscope-activity"></a>CancellationScope 活动

使用 <xref:System.Activities.Statements.CancellationScope> 活动可指定要执行的活动以及该活动的取消逻辑。

### <a name="using-the-cancellationscope-activity-designer"></a>使用 CancellationScope 活动设计器

" **CancellationScope** " 活动设计器可在 "**工具箱**" 的 "**事务**" 类别中找到。 若要打开 **工具箱**，请选择工作流设计器的 " **工具箱** " 选项卡。 或者，从 "**视图**" 菜单中选择 **"工具箱**"，或按**Ctrl** + **Alt** + **X**。

可以将 " **CancellationScope** " 活动设计器从 **"工具箱** " 拖放到工作流设计器图面上放置活动的任何位置，例如中 <xref:System.Activities.Statements.Sequence> 。 删除 " **CancellationScope** " 活动设计器将创建一个 <xref:System.Activities.Statements.CancellationScope> 活动，其默认值 <xref:System.Activities.Activity.DisplayName%2A> 为 CancellationScope。 编辑 " <xref:System.Activities.Activity.DisplayName%2A> **CancellationScope** " 活动设计器的标头中的值。 还可以在属性网格的 " **DisplayName** " 框中对其进行编辑。

### <a name="the-cancellationscope-properties"></a>CancellationScope 属性

下表列出 <xref:System.Activities.Statements.CancellationScope> 属性并说明如何在设计器中使用它们。 <xref:System.Activities.Activity.DisplayName%2A>属性可在属性网格中进行编辑，但其他属性必须在工作流设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.CancellationScope> 活动的可选友好名称。 默认值为 CancellationScope。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.CancellationScope.Body%2A>|正确|指定为其提供取消逻辑的活动。 若要添加 <xref:System.Activities.Statements.CancellationScope.Body%2A> 活动，请将 **"工具箱**" 中的活动拖放到 " **CancellationScope** " 活动设计器的 "**正文**" 框中。 添加提示文本 "在此处放置活动"。|
|<xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>|正确|指定在有取消时执行的活动。 若要添加 <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> 活动，请将活动从 **"工具箱**" 拖放到 " **CancellationScope** " 活动设计器上的 " **CancellationHandler** " 框中。 添加提示文本 "在此处放置活动"。|

## <a name="see-also"></a>另请参阅

- [事务](../workflow-designer/transaction-activity-designers.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [确认](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)
