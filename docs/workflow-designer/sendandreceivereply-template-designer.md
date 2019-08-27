---
title: 工作流设计器-SendAndReceiveReply 模板设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.SendAndReceiveReply.UI
- System.ServiceModel.Activities.ReceiveReply.UI
ms.assetid: 818a8c84-6593-416d-b016-1d91b85ffb68
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e71615e90a23ad8ca6de6e01495de1ea8538a644
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62809539"
---
# <a name="sendandreceivereply-template-designer"></a>SendAndReceiveReply 模板设计器

**SendAndReceiveReply**使用模板来创建一对预配置<xref:System.ServiceModel.Activities.Send>和<xref:System.ServiceModel.Activities.ReceiveReply>活动。 活动属于<xref:System.Activities.Statements.Sequence>活动，并作为客户端上的请求/响应消息交换模式的一部分的关联。

## <a name="the-sendandreceivereply-template"></a>SendAndReceiveReply 模板

添加**SendAndReceiveReply**模板执行除了创建三个操作<xref:System.ServiceModel.Activities.Send>并<xref:System.ServiceModel.Activities.ReceiveReply>中的活动<xref:System.Activities.Statements.Sequence>活动：

- 配置<xref:System.ServiceModel.Activities.Send.OperationName%2A>并<xref:System.ServiceModel.Activities.Send.ServiceContractName%2A>的属性<xref:System.ServiceModel.Activities.Send>活动。

- 将 <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A> 活动的 <xref:System.ServiceModel.Activities.ReceiveReply> 属性绑定到 <xref:System.ServiceModel.Activities.Send> 活动。

- 创建一个 <xref:System.ServiceModel.Activities.CorrelationHandle> 作为父活动中的一个变量。

### <a name="use-the-sendandreceivereply-template-designer"></a>使用 SendAndReceiveReply 模板设计器

访问**SendAndReceiveReply**中的活动设计器**消息传送**类别**工具箱**。 **SendAndReceiveReply**活动设计器可以从拖动**工具箱**和任何通常放置活动的位置放置到工作流设计器图面。 放置在活动设计器创建<xref:System.ServiceModel.Activities.Send>可以使用配置的活动**发送**活动设计器和相关<xref:System.ServiceModel.Activities.ReceiveReply>，可以使用配置**ReceiveReplyForSend**设计器。

有关使用详细信息**发送**设计器配置<xref:System.ServiceModel.Activities.Send>活动，请参阅[发送](../workflow-designer/send-activity-designer.md)。

### <a name="properties-of-receivereply"></a>ReceiveReply 的属性

下表显示<xref:System.ServiceModel.Activities.ReceiveReply>属性并说明它们如何使用在设计器中。 可以在属性网格中编辑这些属性，一些可以在工作流设计器图面上进行编辑。

| 属性名 | 必需 | 用法 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | False | <xref:System.ServiceModel.Activities.ReceiveReply> 活动的可选友好名称。 默认值为 ReceiveReplyForSend。<br /><br /> 虽然对友好使用非默认值<xref:System.Activities.Activity.DisplayName%2A>并不严格要求，最好是使用此类值。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A> | True | 对与此 <xref:System.ServiceModel.Activities.Send> 活动配对的 <xref:System.ServiceModel.Activities.ReceiveReply> 活动的引用。 此属性不能**null**。 在客户端上将 <xref:System.ServiceModel.Activities.Send> 和 <xref:System.ServiceModel.Activities.ReceiveReply> 活动配合使用，可对请求/响应消息模式建模。 此属性指定配对的 <xref:System.ServiceModel.Activities.Send> 活动。 在设计器中，您不能编辑此属性，因为它自动绑定到<xref:System.ServiceModel.Activities.Send>活动从其创建<xref:System.ServiceModel.Activities.ReceiveReply>活动。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.Content%2A> | False | 指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 编辑此属性的旁边单击省略号按钮**内容**在属性网格中，或单击字段**定义**按钮旁边**内容**上的标签**接收**活动设计器图面。 两者都显示**内容定义**对话框。 有关如何使用此框的详细信息，请参阅[内容定义对话框](../workflow-designer/content-definition-dialog-box.md)。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.CorrelationInitializers%2A> | False | 指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Receive> 对象的集合。 单击省略号按钮旁边<xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A>属性在属性网格中，打开**添加相关初始值设定项**对话框。 有关使用此框的详细信息，请参阅[添加相关初始值设定项对话框](../workflow-designer/add-correlationinitializers-dialog-box.md)。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.Action%2A> | False | 指定消息的操作标头。 如果未显式设置，其默认值为：<br /><br /> <strong>https://tempuri.org/{service 协定命名空间} / {服务协定名称} / {操作名称}。</strong> |

## <a name="see-also"></a>请参阅

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [Receive](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [Send](../workflow-designer/send-activity-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)