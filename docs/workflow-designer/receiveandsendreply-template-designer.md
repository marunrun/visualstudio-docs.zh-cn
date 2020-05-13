---
title: 工作流设计器 - 接收和发送回复模板设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.ReceiveAndSendReply.UI
- System.ServiceModel.Activities.SendReply.UI
ms.assetid: d1d9a058-df7e-48f5-a2e7-3caeeba7eaa6
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 042032efe745a9cb38bbf4e362cb5ad8440129ba
ms.sourcegitcommit: d6828e7422c8d74ec1e99146fedf0a05f757245f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "80395302"
---
# <a name="receiveandsendreply-template-designer"></a>ReceiveAndSendReply 模板设计器

**"接收和发送回复"** 模板用于创建一对预配置<xref:System.ServiceModel.Activities.Receive>的活动。 <xref:System.ServiceModel.Activities.SendReply> 活动是活动的一<xref:System.Activities.Statements.Sequence>部分，并作为服务器上的请求/响应消息交换模式的一部分进行关联。

## <a name="the-receiveandsendreply-template"></a>接收和发送回复模板

添加**ReceiveAndSendReply**模板除了创建 具有活动<xref:System.ServiceModel.Activities.Receive>的活动<xref:System.ServiceModel.Activities.SendReply>之外，还有<xref:System.Activities.Statements.Sequence>三件事：

- 配置<xref:System.ServiceModel.Activities.Receive.OperationName%2A><xref:System.ServiceModel.Activities.Receive>活动的 和<xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A>属性。

- 将 <xref:System.ServiceModel.Activities.SendReply.Request%2A> 活动的 <xref:System.ServiceModel.Activities.Receive> 属性绑定到 <xref:System.ServiceModel.Activities.Send> 活动。

- 创建一个 <xref:System.ServiceModel.Activities.CorrelationHandle> 作为父活动中的一个变量。

### <a name="use-the-receiveandsendreply-template-designer"></a>使用接收和发送回复模板设计器

访问**工具箱****"消息"** 类别中的 **"接收和发送回复**"活动设计器。 **接收和发送回复**活动设计器可以从**工具箱**拖动，并放置在工作流设计器表面上，无论活动通常放置在哪里。 删除活动设计器将创建<xref:System.ServiceModel.Activities.Receive>一个活动，该活动可以使用 **"发送活动**设计器"<xref:System.ServiceModel.Activities.SendReply>配置，并创建一个可以使用 SendReplyToReceive 设计器配置的相关活动。

有关使用**接收**设计器配置<xref:System.ServiceModel.Activities.Receive>活动的详细信息，请参阅[接收活动设计器](../workflow-designer/receive-activity-designer.md)。

### <a name="properties-of-sendreply"></a>SendReply 的属性

下表列出 <xref:System.ServiceModel.Activities.SendReply> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中编辑，有些可以在工作流设计器表面上进行编辑。

| 属性名称 | 必选 | 使用情况 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | False | <xref:System.ServiceModel.Activities.SendReply> 活动的可选友好名称。 默认值为 SendReplyToReceive。<br /><br /> 尽管不是严格要求对友好值<xref:System.Activities.Activity.DisplayName%2A>使用非默认值，但最好使用这样的值。 |
| <xref:System.ServiceModel.Activities.SendReply.Request%2A> | True | 对与此 <xref:System.ServiceModel.Activities.Receive> 活动配对的 <xref:System.ServiceModel.Activities.SendReply> 活动的引用。 此属性不能**为 null**。 <xref:System.ServiceModel.Activities.Receive>和<xref:System.ServiceModel.Activities.SendReply>活动一起使用在服务器上建模请求/响应消息传递模式。 此属性指定配对的 <xref:System.ServiceModel.Activities.Send> 活动。 在设计器中，无法编辑此属性，因为它会自动绑定到您从中创建活动<xref:System.ServiceModel.Activities.Send>的活动。 <xref:System.ServiceModel.Activities.SendReply> |
| <xref:System.ServiceModel.Activities.SendReply.Content%2A> | False | 指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 通过单击属性网格中 **"内容"** 字段旁边的省略号按钮，或单击 **"接收**活动设计器"图名图人曲面上 **"内容**"标签旁边的 **"定义"** 按钮来编辑此属性。 两者都显示 **"内容定义"** 对话框。 有关如何使用此框的详细信息，请参阅[内容定义对话框主题](../workflow-designer/content-definition-dialog-box.md)。 |
| <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> | False | 指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Receive> 对象的集合。 单击属性网格中<xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A>属性旁边的省略号按钮以打开"**添加关联初始化器"** 对话框。 有关使用此框的详细信息，请参阅[添加关联初始程序对话框主题](../workflow-designer/add-correlationinitializers-dialog-box.md)。 |
| <xref:System.ServiceModel.Activities.SendReply.Action%2A> | False | 指定消息的操作标头。 如果未显式设置，则其值默认为：<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}` |
| <xref:System.ServiceModel.Activities.SendReply.PersistBeforeSend%2A> | False | 指定在发送回复消息前是否应保留工作流实例。 默认值为“false”****。 |

## <a name="see-also"></a>请参阅

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [收到](../workflow-designer/receive-activity-designer.md)
- [发送](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)