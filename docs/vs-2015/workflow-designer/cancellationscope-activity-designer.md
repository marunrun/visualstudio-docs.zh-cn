---
title: CancellationScope 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.CancellationScope.UI
ms.assetid: 2c85d663-b219-4142-9866-7693ffd46379
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 6207d1fcd2e920de979a13624e5cf1b442c2703c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977201"
---
# <a name="cancellationscope-activity-designer"></a>CancellationScope 活动设计器
**CancellationScope**活动设计器用于创建和配置<xref:System.Activities.Statements.CancellationScope>活动。  
  
## <a name="the-cancellationscope-activity"></a>CancellationScope 活动  
 使用 <xref:System.Activities.Statements.CancellationScope> 活动可指定要执行的活动以及该活动的取消逻辑。  
  
### <a name="using-the-cancellationscope-activity-designer"></a>使用 CancellationScope 活动设计器  
 **CancellationScope**活动设计器可在**事务**类别**工具箱**，这通过单击来访问**工具箱**选项卡[!INCLUDE[wfd2](../includes/wfd2-md.md)](或者，选择**工具栏**从**视图**菜单或 CTRL + ALT + X。)  
  
 **CancellationScope**活动设计器可以从拖动**工具箱**拖放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面上任何位置通常放置活动的例如内<xref:System.Activities.Statements.Sequence>。 这将创建具有 CancellationScope 的默认 <xref:System.Activities.Statements.CancellationScope> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 <xref:System.Activities.Activity.DisplayName%2A>值可以在的标头中编辑**CancellationScope**活动设计器中或在**DisplayName**属性网格的框。  
  
### <a name="the-cancellationscope-properties"></a>CancellationScope 属性  
 下表列出 <xref:System.Activities.Statements.CancellationScope> 属性并说明如何在设计器中使用它们。 <xref:System.Activities.Activity.DisplayName%2A> 属性可在属性网格中编辑，但其他属性必须在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上进行编辑。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.CancellationScope> 活动的可选友好名称。 默认值为 CancellationScope。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|  
|<xref:System.Activities.Statements.CancellationScope.Body%2A>|True|指定为其提供取消逻辑的活动。 若要添加<xref:System.Activities.Statements.CancellationScope.Body%2A>活动，请将活动从拖**工具箱**到**正文**框**CancellationScope**带提示文本"放置活动设计器在此处活动"。|  
|<xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>|True|指定在取消事件中执行的活动。 若要添加<xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>活动，请将活动从拖**工具箱**到**CancellationHandler**框**CancellationScope**附带提示的活动设计器文本"此处放置活动"。|  
  
## <a name="see-also"></a>请参阅  
 [事务](../workflow-designer/transaction-activity-designers.md)   
 [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)   
 [补偿](../workflow-designer/compensate-activity-designer.md)   
 [Confirm](../workflow-designer/confirm-activity-designer.md)   
 [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)