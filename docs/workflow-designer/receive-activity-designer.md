---
title: 工作流设计器接收活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.Receive.UI
ms.assetid: f58d3c70-944d-4bb4-90a7-e68c103caddc
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 55f49a32036fcfd5e9f75f3d8dd61499c4af0b2e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86875717"
---
# <a name="receive-activity-designer"></a>Receive 活动设计器

" **接收** " 活动设计器用于创建和配置 <xref:System.ServiceModel.Activities.Receive> 活动。 <xref:System.ServiceModel.Activities.Receive> 活动是接收消息的活动，可接收的消息包括内置类型（如 <xref:System.ServiceModel.Channels.Message>、<xref:System.IO.Stream> 或 <xref:System.Xml.Linq.XElement>）或者应用程序定义的数据协定、消息协定或可序列化的 XML 类。

## <a name="the-receive-activity"></a>Receive 活动

<xref:System.ServiceModel.Activities.Receive> 活动可以接收一个或多个项，具体取决于所用接收内容的类型。 <xref:System.ServiceModel.Activities.SendReply> 活动可绑定到作为服务上请求/响应消息交换模式的一部分接收消息的 <xref:System.ServiceModel.Activities.Receive> 活动。

### <a name="using-the-receive-activity-designer"></a>使用 Receive 活动设计器

访问 "**工具箱**" 的 "**消息传送**" 类别中的 "**接收**" 活动设计器。 可以将 " **接收** " 活动设计器从 " **工具箱** " 拖放到工作流设计器图面上通常放置活动的任何位置。 这将创建具有 Receive 的默认 <xref:System.ServiceModel.Activities.Receive> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在 "**接收**" 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑。

若要创建 <xref:System.ServiceModel.Activities.SendReply> 活动并将其绑定到所选 <xref:System.ServiceModel.Activities.Receive> 活动，请右键单击 " **接收** " 活动设计器，单击上下文菜单中的 " **创建 SendReply** " 项，" **SendReplyToReceive** " 设计器将显示在 **接收** 设计器下。 <xref:System.ServiceModel.Activities.SendReply> 活动是作为服务上请求/响应消息交换模式的一部分发送答复消息的一个活动。 可以通过 **SendReplyToReceive** 设计器进行配置。

或者，"**工具箱**" 的 "**消息传送**" 类别中的 " **ReceiveAndSendReply** " 模板设计器可用于创建一对预配置的 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动。 有关使用 **ReceiveAndSendReply** 和 **SendReplyToReceive** 模板的详细信息，请参阅 [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md) 主题。

### <a name="the-receive-activity-properties"></a>Receive 活动属性

下表列出 <xref:System.ServiceModel.Activities.Receive> 属性并说明如何在设计器中使用它们。 这些属性可以在 "属性" 网格中编辑，也可以在工作流设计器图面上编辑。 唯一必需的属性是 <xref:System.ServiceModel.Activities.Receive.OperationName%2A> 属性。

| 属性名称 | 必选 | 使用情况 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | 错误 | 指定 <xref:System.ServiceModel.Activities.Receive> 活动的友好名称。 默认值为 Receive。<br /><br /> 虽然对友好 <xref:System.Activities.Activity.DisplayName%2A> 使用非默认值不是绝对必需的，但最好使用非默认值。 |
| <xref:System.ServiceModel.Activities.Receive.OperationName%2A> | 正确 | 指定由此 <xref:System.ServiceModel.Activities.Receive> 活动实现的服务操作的名称。 如果未显式设置**操作**属性，则此属性用于构造**操作**属性的默认值。 |
| <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> | 错误 | 指定服务协定的名称。 此属性用于将服务操作分组至各个服务协定。 所有具有相同的 <xref:System.ServiceModel.Activities.Receive> 的 <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> 活动都分组到同一服务协定（WSDL 端口类型）中。 默认值为顶层 (根) 活动的完全限定的 CLR 名称。 |
| <xref:System.ServiceModel.Activities.Receive.Content%2A> | 错误 | 指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 若要编辑此属性，请在属性网格中选择 "**内容**" 字段旁边的省略号按钮，或单击 "**接收**" 活动设计器图面上**内容**标签旁边的 "**定义 ...** " 按钮。 两者都显示 " **内容定义** " 对话框。 有关如何使用此框的详细信息，请参阅 " [内容定义" 对话框](../workflow-designer/content-definition-dialog-box.md) 主题。 |
| <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> | 错误 | 使用 <xref:System.ServiceModel.Activities.Receive> 对象指定工作流的服务操作中各 <xref:System.ServiceModel.MessageQuerySet> 活动之间的关联。 在 "属性" 网格中单击属性旁的省略号按钮， <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> 以打开 " **CorrelatesOn 定义** " 对话框。 有关使用此对话框的详细信息，请参阅 " [内容定义" 对话框](../workflow-designer/content-definition-dialog-box.md) 主题。 |
| <xref:System.ServiceModel.Activities.Receive.CorrelatesWith%2A> | 错误 | 指定用于将消息路由到相应工作流实例的 <xref:System.ServiceModel.Activities.CorrelationHandle>。<br /><br /> 在 "属性" 网格中单击属性旁的省略号按钮， <xref:System.ServiceModel.Activities.Receive.CorrelatesWith%2A> 以打开 " **表达式编辑器** " 对话框。 有关使用此对话框的详细信息，请参阅 [如何：使用表达式编辑器](../workflow-designer/how-to-use-the-expression-editor.md) 主题。 |
| <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> | 错误 | 指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Receive> 对象的集合。 在 "属性" 网格中单击属性旁的省略号按钮， <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> 以打开 " **添加相关初始值设定项** " 对话框。 有关使用此框的详细信息，请参阅 [Add CorrelationInitializers 对话框](../workflow-designer/add-correlationinitializers-dialog-box.md) 主题。 |
| <xref:System.ServiceModel.Activities.Receive.CanCreateInstance%2A> | 错误 | 指定一个值，该值确定如果消息未关联到现有的工作流实例，是否创建一个新工作流实例来处理该消息。 如果将该值设置为 **true**，则将创建一个新的工作流实例来处理该消息，而不会将该消息与现有的工作流实例相关联。 |
| <xref:System.ServiceModel.Activities.Receive.KnownTypes%2A> | 错误 | 指定由此 <xref:System.ServiceModel.Activities.Receive> 活动实现的服务操作的已知类型集合。 此属性应与设置为 <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> 的 <xref:System.Runtime.Serialization.DataContractSerializer> 属性结合使用。 如果使用了 <xref:System.Xml.Serialization.XmlSerializer>，则忽略此项。<br /><br /> 选择 "属性网格" 中 " **KnownTypes** " 字段旁边的省略号按钮，以显示可以添加相关类型的 " **类型集合编辑器** " 对话框。 有关使用此框的详细信息，请参阅 " [类型集合编辑器" 对话框](../workflow-designer/type-collection-editor-dialog-box.md) 主题。 |
| <xref:System.ServiceModel.Activities.Receive.ProtectionLevel%2A> | 错误 | 指定消息的 <xref:System.Net.Security.ProtectionLevel>。<br /><br /> 1.  <xref:System.Net.Security.ProtectionLevel> 表示仅限身份验证。<br />2.  <xref:System.Net.Security.ProtectionLevel> 表示签名数据，以帮助确保所传输数据的完整性。<br />3.  <xref:System.Net.Security.ProtectionLevel> 表示对数据进行加密和签名，以帮助确保所传输数据的保密性和完整性。 |
| <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> | 错误 | 指定 <xref:System.ServiceModel.Activities.Receive> 活动实现的服务操作所使用的序列化程序的类型。 默认值为 <xref:System.Runtime.Serialization.DataContractSerializer>，它使用提供的数据协定将类型实例序列化和反序列化为 XML 流或文档。 如果需要对 XML 进行更多控制，还可使用 <xref:System.Xml.Serialization.XmlSerializer>。 |
| <xref:System.ServiceModel.Activities.Receive.Action%2A> | 错误 | 指定消息的操作标头。 如果未显式设置，则其值默认为： `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}` 。 |

## <a name="see-also"></a>另请参阅

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [发送](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)
