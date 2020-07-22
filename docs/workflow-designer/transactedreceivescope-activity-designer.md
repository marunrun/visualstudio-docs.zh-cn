---
title: 工作流设计器 TransactedReceiveScope 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.TransactedReceiveScope.UI
ms.assetid: 7ca93aad-4e83-4d81-90f4-998ee114d9b6
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 75fb1da392bce7dbd0cd7849d83b3b452521e0c7
ms.sourcegitcommit: 186c0c250d85ac74274fa1e438b4c7c7108d8a36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86875925"
---
# <a name="transactedreceivescope-activity-designer"></a>TransactedReceiveScope 活动设计器

**TransactedReceiveScope**设计器用于创建和配置 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 活动。

## <a name="the-transactedreceivescope-activity"></a>TransactedReceiveScope 活动

<xref:System.ServiceModel.Activities.TransactedReceiveScope> 活动使你能够将事务流动到工作流或调度程序创建的服务器事务中。

### <a name="using-the-transactedreceivescope-activity-designer"></a>使用 TransactedReceiveScope 活动设计器

访问 "**工具箱**" 的 "**消息传送**" 类别中的 " **TransactedReceiveScope** " 活动设计器。 可以将 " **TransactedReceiveScope** " 活动设计器从 "**工具箱**" 拖放到工作流设计器图面上通常放置活动的任何位置。 这将创建 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 具有 TransactedReceiveScope 的默认**DisplayName**的活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在 " **TransactedReceiveScope** " 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑。

**TransactedReceiveScope**设计器包含 "**请求**" 和 "**正文**" 框。 它们用于配置 <xref:System.ServiceModel.Activities.TransactedReceiveScope.Request%2A> 属性，该属性指定一个 <xref:System.ServiceModel.Activities.Receive> 活动和一个指定某些其他 <xref:System.ServiceModel.Activities.TransactedReceiveScope.Body%2A> 的 <xref:System.Activities.Activity> 属性。 <xref:System.ServiceModel.Activities.TransactedReceiveScope.Request%2A> 创建一个事务。 然后使该事务成为 <xref:System.ServiceModel.Activities.TransactedReceiveScope.Body%2A> 范围的环境事务以便此范围中的任何活动可在该事务内执行。

### <a name="the-transactedreceivescope-properties"></a>TransactedReceiveScope 属性

下表列出 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 属性并说明如何在设计器中使用它们。 这些 <xref:System.Activities.Activity.DisplayName%2A> 属性可以在属性网格中或工作流设计器图面上进行编辑，但其他属性必须在设计图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.ServiceModel.Activities.TransactedReceiveScope> 活动的可选友好名称。 默认值为 TransactedReceiveScope。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 名称不是绝对必需的，但最好使用显示名称。|
|<xref:System.ServiceModel.Activities.TransactedReceiveScope.Request%2A>|正确|<xref:System.ServiceModel.Activities.Receive>将活动放置在活动设计器图面上的**请求**块中。|
|<xref:System.ServiceModel.Activities.TransactedReceiveScope.Body%2A>|错误|将拖 <xref:System.Activities.Activity> 放到活动设计器图面上的**主体**块中。|

## <a name="see-also"></a>另请参阅

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [收](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [发送](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)