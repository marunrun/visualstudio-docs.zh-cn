---
title: 工作流设计器-发送活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.Send.UI
ms.assetid: b514f2e4-767c-4b94-ac61-dd3a54d4b96d
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8d27bd9be1b769215dd77d1e906a5698e17bd18b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63009124"
---
# <a name="send-activity-designer"></a>Send 活动设计器

**发送**活动设计器用于创建和配置<xref:System.ServiceModel.Activities.Send>活动。

## <a name="the-send-activity"></a>Send 活动

 <xref:System.ServiceModel.Activities.Send> 活动用于向服务发送消息。 作为客户端上请求/响应消息交换模式的一部分接收消息的 <xref:System.ServiceModel.Activities.ReceiveReply> 活动可绑定到 <xref:System.ServiceModel.Activities.Send> 活动。

### <a name="using-the-send-activity-designer"></a>使用 Send 活动设计器

访问**发送**中的活动设计器**消息传送**类别**工具箱**。 **发送**活动设计器可以从拖动**工具箱**和任何通常放置活动的位置放置到工作流设计器图面。 这将创建具有 Send 的默认 <xref:System.ServiceModel.Activities.Send> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在的标头中编辑**发送**活动设计器中或在**DisplayName**属性网格的框。

若要创建<xref:System.ServiceModel.Activities.ReceiveReply>活动并将其绑定到所选<xref:System.ServiceModel.Activities.Send>活动中，右键单击**发送**活动设计器中，单击**创建 ReceiveReply**的上下文菜单中的项和**ReceiveReplyForSend**如下所示设计器**发送**设计器。 <xref:System.ServiceModel.Activities.ReceiveReply> 活动是作为客户端上请求/响应消息交换模式的一部分接收消息的一个活动。 可以使用配置**ReceiveReplyForSend**设计器。

或者， **SendAndReceiveReply**中的模板设计器**消息传送**类别**工具箱**可用于创建一对预配置<xref:System.ServiceModel.Activities.Send>和<xref:System.ServiceModel.Activities.ReceiveReply>活动。 有关使用详细信息**SendAndReceiveReply**并**ReceiveReplyForSend**模板，请参阅[SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)主题。

### <a name="the-send-activity-properties"></a>Send 活动属性

下表列出 <xref:System.ServiceModel.Activities.Send> 属性并说明如何在设计器中使用它们。 在属性网格中或在工作流设计器图面上，可以编辑这些属性。

| 属性名 | 必需 | 用法 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | False | <xref:System.ServiceModel.Activities.Send> 活动的友好名称。 默认值为 Send。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。 |
| <xref:System.ServiceModel.Activities.Send.OperationName%2A> | True | 由此 <xref:System.ServiceModel.Activities.Send> 活动调用的服务操作的名称。 此属性用于构造的默认值为**操作**属性如果**操作**属性未显式设置。 |
| <xref:System.ServiceModel.Activities.Send.ServiceContractName%2A> | True | 实现了要调用的服务的服务协定的名称。 |
| <xref:System.ServiceModel.Activities.Send.Content%2A> | False | 指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 编辑此属性通过选择旁的省略号按钮**内容**字段在属性网格或单击**定义...** 按钮旁边**内容**上的标签**接收**活动设计器图面。 两者都显示**内容定义**对话框。 有关如何使用此框的详细信息，请参阅[内容定义对话框](../workflow-designer/content-definition-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.Send.CorrelatesWith%2A> | False | 指定用于将消息路由到相应工作流实例的 <xref:System.ServiceModel.Activities.CorrelationHandle>。<br /><br /> 单击省略号按钮旁边<xref:System.ServiceModel.Activities.Send.CorrelatesWith%2A>属性在属性网格中，打开**表达式编辑器**对话框。 有关使用此对话框的详细信息，请参阅[如何：使用表达式编辑器](../workflow-designer/how-to-use-the-expression-editor.md)主题。 |
| <xref:System.ServiceModel.Activities.Send.CorrelationInitializers%2A> | False | 指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Send> 对象的集合。 单击省略号按钮旁边<xref:System.ServiceModel.Activities.Send.CorrelationInitializers%2A>属性在属性网格中，打开**添加相关初始值设定项**对话框。 有关使用此框的详细信息，请参阅[添加相关初始值设定项对话框](../workflow-designer/add-correlationinitializers-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.Send.KnownTypes%2A> | False | 此 <xref:System.ServiceModel.Activities.Send> 活动要调用的服务操作的已知类型集合。 此属性应与设置为 <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> 的 <xref:System.Runtime.Serialization.DataContractSerializer> 属性结合使用。 如果使用了 <xref:System.Xml.Serialization.XmlSerializer>，则忽略此项。<br /><br /> 选择旁的省略号按钮**KnownTypes**字段中要显示的属性网格**类型集合编辑器**对话框可以添加相关类型。<br /><br /> 选择旁的省略号按钮**KnownTypes**字段中要显示的属性网格**类型集合编辑器**对话框可以添加相关类型。 有关使用此框的详细信息，请参阅[类型集合编辑器对话框](../workflow-designer/type-collection-editor-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.Send.ProtectionLevel%2A> | True | 指定消息的 <xref:System.Net.Security.ProtectionLevel>。<br /><br /> 1。<xref:System.Net.Security.ProtectionLevel>意味着仅使用身份验证。<br />2。<xref:System.Net.Security.ProtectionLevel>意味着登录数据，以帮助确保传输数据的完整性。<br />3。<xref:System.Net.Security.ProtectionLevel>方法进行加密和签名数据，以帮助确保保密性和传输数据的完整性。 |
| <xref:System.ServiceModel.Activities.Send.SerializerOption%2A> | True | <xref:System.ServiceModel.Activities.Send> 活动要调用的服务操作所用的序列化程序。 默认值为 <xref:System.Runtime.Serialization.DataContractSerializer>，它使用提供的数据协定将类型实例序列化和反序列化为 XML 流或文档。 |
| <xref:System.ServiceModel.Activities.Send.Action%2A> | False | 指定消息的操作标头。 如果显式设置，其默认值为： https://tempuri.org/{service协定命名空间} / {服务协定名称} / {操作名称}。 如果该值是对 <xref:System.ServiceModel.Activities.Send> 活动指定的，则接收消息的 <xref:System.ServiceModel.Activities.Receive> 活动必须具有同一值才能正确传递该消息。 |
| <xref:System.ServiceModel.Activities.Send.TokenImpersonationLevel%2A> | | <xref:System.Security.Principal.TokenImpersonationLevel> 可用于消息的接收方。 它定义安全模拟级别，控制到的服务器进程可以代表客户端进程执行操作的程度。<xref:System.Security.Principal.TokenImpersonationLevel> 指示未分配模拟级别。 <xref:System.Security.Principal.TokenImpersonationLevel> 指示服务器进程无法获取有关客户端的标识信息，且无法模拟客户端。 <xref:System.Security.Principal.TokenImpersonationLevel> 指示服务器进程可以获取有关客户端的信息（如安全标识符和特权），但它无法模拟客户端。 这对于导出自身对象的服务器非常有用，例如，导出表和视图的数据库产品。 在不能使用其他正使用客户端安全上下文的服务的情况下，服务器可以使用检索到的客户端安全信息做出访问验证决策。 <xref:System.Security.Principal.TokenImpersonationLevel> 指示服务器进程可以在其本地系统上模拟客户端的安全上下文。 服务器无法在远程系统上模拟客户端。 <xref:System.Security.Principal.TokenImpersonationLevel> 指示服务器进程可以在远程系统上模拟客户端的安全上下文。 |
| <xref:System.ServiceModel.Activities.Send.Endpoint%2A> | | <xref:System.ServiceModel.Endpoint> 活动要将消息发送到的 <xref:System.ServiceModel.Activities.Send>。 如果设置此属性<xref:System.ServiceModel.Activities.Send.EndpointConfigurationName%2A>属性应**null**。 |
| <xref:System.ServiceModel.Activities.Send.EndpointAddress%2A> | | 要将消息发送到的 <xref:System.ServiceModel.EndpointAddress>。 |
| <xref:System.ServiceModel.Activities.Send.EndpointConfigurationName%2A> | | 终结点配置的名称。 在配置文件中配置终结点时设置此属性。 此属性应设置为给定的名称**\<终结点 >** 配置文件中的元素。 如果设置此属性，<xref:System.ServiceModel.Activities.Send.Endpoint%2A>属性应**null**。 |

## <a name="see-also"></a>请参阅

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [Receive](../workflow-designer/receive-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)