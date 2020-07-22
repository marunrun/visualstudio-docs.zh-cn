---
title: 工作流设计器发送活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.Send.UI
ms.assetid: b514f2e4-767c-4b94-ac61-dd3a54d4b96d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dd1eff0a52dfb258d7f7af49b03543fd741bc88c
ms.sourcegitcommit: 186c0c250d85ac74274fa1e438b4c7c7108d8a36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86875951"
---
# <a name="send-activity-designer"></a>Send 活动设计器

"**发送**" 活动设计器用于创建和配置 <xref:System.ServiceModel.Activities.Send> 活动。

## <a name="the-send-activity"></a>Send 活动

 <xref:System.ServiceModel.Activities.Send> 活动用于向服务发送消息。 作为客户端上请求/响应消息交换模式的一部分接收消息的 <xref:System.ServiceModel.Activities.ReceiveReply> 活动可绑定到 <xref:System.ServiceModel.Activities.Send> 活动。

### <a name="using-the-send-activity-designer"></a>使用 Send 活动设计器

访问 "**工具箱**" 的 "**消息传送**" 类别中的 " **Send** " 活动设计器。 可以将 "**发送**" 活动设计器从 "**工具箱**" 拖放到工作流设计器图面上通常放置活动的任何位置。 这将创建具有 Send 的默认 <xref:System.ServiceModel.Activities.Send> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在 " **Send** " 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑。

若要创建 <xref:System.ServiceModel.Activities.ReceiveReply> 活动并将其绑定到所选 <xref:System.ServiceModel.Activities.Send> 活动，请右键单击 " **Send** " 活动设计器，在上下文菜单中单击 "**创建 ReceiveReply** " 项， **ReceiveReplyForSend**设计器将显示在**发送**设计器下。 <xref:System.ServiceModel.Activities.ReceiveReply> 活动是作为客户端上请求/响应消息交换模式的一部分接收消息的一个活动。 可以通过**ReceiveReplyForSend**设计器进行配置。

或者，"**工具箱**" 的 "**消息传送**" 类别中的 " **SendAndReceiveReply** " 模板设计器可用于创建一对预配置的 <xref:System.ServiceModel.Activities.Send> 和 <xref:System.ServiceModel.Activities.ReceiveReply> 活动。 有关使用**SendAndReceiveReply**和**ReceiveReplyForSend**模板的详细信息，请参阅[SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)主题。

### <a name="the-send-activity-properties"></a>Send 活动属性

下表列出 <xref:System.ServiceModel.Activities.Send> 属性并说明如何在设计器中使用它们。 这些属性可以在 "属性" 网格中编辑，也可以在工作流设计器图面上编辑。

| 属性名称 | 必选 | 使用情况 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | 错误 | <xref:System.ServiceModel.Activities.Send> 活动的友好名称。 默认值为 Send。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。 |
| <xref:System.ServiceModel.Activities.Send.OperationName%2A> | 正确 | 由此 <xref:System.ServiceModel.Activities.Send> 活动调用的服务操作的名称。 如果未显式设置**操作**属性，则此属性用于构造**操作**属性的默认值。 |
| <xref:System.ServiceModel.Activities.Send.ServiceContractName%2A> | 正确 | 实现了要调用的服务的服务协定的名称。 |
| <xref:System.ServiceModel.Activities.Send.Content%2A> | 错误 | 指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 若要编辑此属性，请在属性网格中选择 "**内容**" 字段旁边的省略号按钮，或单击 "**接收**" 活动设计器图面上**内容**标签旁边的 "**定义 ...** " 按钮。 两者都显示 "**内容定义**" 对话框。 有关如何使用此框的详细信息，请参阅 "[内容定义" 对话框](../workflow-designer/content-definition-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.Send.CorrelatesWith%2A> | 错误 | 指定用于将消息路由到相应工作流实例的 <xref:System.ServiceModel.Activities.CorrelationHandle>。<br /><br /> 在 "属性" 网格中单击属性旁的省略号按钮， <xref:System.ServiceModel.Activities.Send.CorrelatesWith%2A> 以打开 "**表达式编辑器**" 对话框。 有关使用此对话框的详细信息，请参阅[如何：使用表达式编辑器](../workflow-designer/how-to-use-the-expression-editor.md)主题。 |
| <xref:System.ServiceModel.Activities.Send.CorrelationInitializers%2A> | 错误 | 指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Send> 对象的集合。 在 "属性" 网格中单击属性旁的省略号按钮， <xref:System.ServiceModel.Activities.Send.CorrelationInitializers%2A> 以打开 "**添加相关初始值设定项**" 对话框。 有关使用此框的详细信息，请参阅[Add CorrelationInitializers 对话框](../workflow-designer/add-correlationinitializers-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.Send.KnownTypes%2A> | 错误 | 此 <xref:System.ServiceModel.Activities.Send> 活动要调用的服务操作的已知类型集合。 此属性应与设置为 <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> 的 <xref:System.Runtime.Serialization.DataContractSerializer> 属性结合使用。 如果使用了 <xref:System.Xml.Serialization.XmlSerializer>，则忽略此项。<br /><br /> 选择 "属性网格" 中 " **KnownTypes** " 字段旁边的省略号按钮，以显示可用于添加相关类型的 "**类型集合编辑器**" 对话框。<br /><br /> 选择 "属性网格" 中 " **KnownTypes** " 字段旁边的省略号按钮，以显示可以添加相关类型的 "**类型集合编辑器**" 对话框。 有关使用此框的详细信息，请参阅 "[类型集合编辑器" 对话框](../workflow-designer/type-collection-editor-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.Send.ProtectionLevel%2A> | 正确 | 指定消息的 <xref:System.Net.Security.ProtectionLevel>。<br /><br /> 1. <xref:System.Net.Security.ProtectionLevel> 表示仅限身份验证。<br />2. <xref:System.Net.Security.ProtectionLevel> 表示签名数据，以帮助确保所传输数据的完整性。<br />3. <xref:System.Net.Security.ProtectionLevel> 表示对数据进行加密和签名，以帮助确保所传输数据的保密性和完整性。 |
| <xref:System.ServiceModel.Activities.Send.SerializerOption%2A> | 正确 | <xref:System.ServiceModel.Activities.Send> 活动要调用的服务操作所用的序列化程序。 默认值为 <xref:System.Runtime.Serialization.DataContractSerializer>，它使用提供的数据协定将类型实例序列化和反序列化为 XML 流或文档。 |
| <xref:System.ServiceModel.Activities.Send.Action%2A> | 错误 | 指定消息的操作标头。 如果未显式设置，则其值默认为： `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}` 。 如果该值是对 <xref:System.ServiceModel.Activities.Send> 活动指定的，则接收消息的 <xref:System.ServiceModel.Activities.Receive> 活动必须具有同一值才能正确传递该消息。 |
| <xref:System.ServiceModel.Activities.Send.TokenImpersonationLevel%2A> | | <xref:System.Security.Principal.TokenImpersonationLevel> 可用于消息的接收方。 它定义安全模拟级别，这些级别控制服务器进程可以代表客户端进程执行的程度。<xref:System.Security.Principal.TokenImpersonationLevel>  指示未分配模拟级别。 <xref:System.Security.Principal.TokenImpersonationLevel>指示服务器进程无法获取有关客户端的标识信息，并且不能模拟客户端。 <xref:System.Security.Principal.TokenImpersonationLevel>指示服务器进程可以获取有关客户端的信息（如安全标识符和特权），但它无法模拟客户端。 这对于导出自身对象的服务器非常有用，例如，导出表和视图的数据库产品。 在不能使用其他正使用客户端安全上下文的服务的情况下，服务器可以使用检索到的客户端安全信息做出访问验证决策。 <xref:System.Security.Principal.TokenImpersonationLevel>指示服务器进程可以在其本地系统上模拟客户端的安全上下文。 服务器无法在远程系统上模拟客户端。 <xref:System.Security.Principal.TokenImpersonationLevel>指示服务器进程可以在远程系统上模拟客户端的安全上下文。 |
| <xref:System.ServiceModel.Activities.Send.Endpoint%2A> | | <xref:System.ServiceModel.Endpoint> 活动要将消息发送到的 <xref:System.ServiceModel.Activities.Send>。 如果设置此属性，则该 <xref:System.ServiceModel.Activities.Send.EndpointConfigurationName%2A> 属性应为**null**。 |
| <xref:System.ServiceModel.Activities.Send.EndpointAddress%2A> | | 要将消息发送到的 <xref:System.ServiceModel.EndpointAddress>。 |
| <xref:System.ServiceModel.Activities.Send.EndpointConfigurationName%2A> | | 端点配置的名称。 在配置文件中配置终结点时设置此属性。 应将此属性设置为配置文件的元素中给定的名称 **\<endpoint>** 。 如果设置此属性，则该 <xref:System.ServiceModel.Activities.Send.Endpoint%2A> 属性应为**null**。 |

## <a name="see-also"></a>另请参阅

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [收](../workflow-designer/receive-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)