---
title: 工作流设计器 ReceiveAndSendReply 模板设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.ReceiveAndSendReply.UI
- System.ServiceModel.Activities.SendReply.UI
ms.assetid: d1d9a058-df7e-48f5-a2e7-3caeeba7eaa6
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 66822664766ac64e466882fda27906f56ebb4aad
ms.sourcegitcommit: 186c0c250d85ac74274fa1e438b4c7c7108d8a36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86876003"
---
# <a name="receiveandsendreply-template-designer"></a>ReceiveAndSendReply 模板设计器

**ReceiveAndSendReply**模板用于创建一对预配置的 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动。 活动是活动的一部分 <xref:System.Activities.Statements.Sequence> ，与服务器上的请求/响应消息交换模式的一部分相关。

## <a name="the-receiveandsendreply-template"></a>ReceiveAndSendReply 模板

除了使用活动创建和活动外，添加**ReceiveAndSendReply**模板还执行三个操作 <xref:System.ServiceModel.Activities.Receive> <xref:System.ServiceModel.Activities.SendReply> <xref:System.Activities.Statements.Sequence> ：

- 配置 <xref:System.ServiceModel.Activities.Receive.OperationName%2A> 活动的和 <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> 属性 <xref:System.ServiceModel.Activities.Receive> 。

- 将 <xref:System.ServiceModel.Activities.SendReply.Request%2A> 活动的 <xref:System.ServiceModel.Activities.Receive> 属性绑定到 <xref:System.ServiceModel.Activities.Send> 活动。

- 创建一个 <xref:System.ServiceModel.Activities.CorrelationHandle> 作为父活动中的一个变量。

### <a name="use-the-receiveandsendreply-template-designer"></a>使用 ReceiveAndSendReply 模板设计器

访问 "**工具箱**" 的 "**消息传送**" 类别中的 " **ReceiveAndSendReply** " 活动设计器。 可以将 " **ReceiveAndSendReply** " 活动设计器从 "**工具箱**" 拖放到工作流设计器图面上通常放置活动的任何位置。 删除活动设计器将创建一个 <xref:System.ServiceModel.Activities.Receive> 活动，该活动可使用 "**发送**活动设计器" 和 <xref:System.ServiceModel.Activities.SendReply> 可使用 SendReplyToReceive 设计器进行配置的相关配置。

有关使用**接收**设计器配置活动的详细信息 <xref:System.ServiceModel.Activities.Receive> ，请参阅[receive 活动设计器](../workflow-designer/receive-activity-designer.md)。

### <a name="properties-of-sendreply"></a>SendReply 的属性

下表列出 <xref:System.ServiceModel.Activities.SendReply> 属性并说明如何在设计器中使用它们。 这些属性可以在 "属性" 网格中进行编辑，某些属性可以在工作流设计器图面上进行编辑。

| 属性名称 | 必选 | 使用情况 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | 错误 | <xref:System.ServiceModel.Activities.SendReply> 活动的可选友好名称。 默认值为 SendReplyToReceive。<br /><br /> 尽管不需要为友好使用非默认值 <xref:System.Activities.Activity.DisplayName%2A> ，但最好使用此类值。 |
| <xref:System.ServiceModel.Activities.SendReply.Request%2A> | 正确 | 对与此 <xref:System.ServiceModel.Activities.Receive> 活动配对的 <xref:System.ServiceModel.Activities.SendReply> 活动的引用。 此属性不能为**null**。 <xref:System.ServiceModel.Activities.Receive>和 <xref:System.ServiceModel.Activities.SendReply> 活动在服务器上一起使用，以对请求/响应消息模式进行建模。 此属性指定配对的 <xref:System.ServiceModel.Activities.Send> 活动。 在设计器中，不能编辑此属性，因为它自动绑定到 <xref:System.ServiceModel.Activities.Send> 您在其中创建了活动的活动 <xref:System.ServiceModel.Activities.SendReply> 。 |
| <xref:System.ServiceModel.Activities.SendReply.Content%2A> | 错误 | 指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 若要编辑此属性，请单击 "属性网格" 中 "**内容**" 字段旁边的省略号按钮，或单击 "**接收**" 活动设计器图面上 "**内容**" 标签旁的 "**定义**" 按钮。 两者都显示 "**内容定义**" 对话框。 有关如何使用此框的详细信息，请参阅 "[内容定义" 对话框](../workflow-designer/content-definition-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> | 错误 | 指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Receive> 对象的集合。 在 "属性" 网格中单击属性旁的省略号按钮， <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> 以打开 "**添加相关初始值设定项**" 对话框。 有关使用此框的详细信息，请参阅[Add CorrelationInitializers 对话框](../workflow-designer/add-correlationinitializers-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.SendReply.Action%2A> | 错误 | 指定消息的操作标头。 如果未显式设置，则其值默认为：<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}` |
| <xref:System.ServiceModel.Activities.SendReply.PersistBeforeSend%2A> | 错误 | 指定在发送回复消息前是否应保留工作流实例。 默认值是 **false**秒。 |

## <a name="see-also"></a>另请参阅

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [收](../workflow-designer/receive-activity-designer.md)
- [发送](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)