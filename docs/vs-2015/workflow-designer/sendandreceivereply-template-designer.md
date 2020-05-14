---
title: 发送和接收回复模板设计器 |微软文档
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.SendAndReceiveReply.UI
- System.ServiceModel.Activities.ReceiveReply.UI
ms.assetid: 818a8c84-6593-416d-b016-1d91b85ffb68
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1bfe43f410709a924b0ebdb0cf6afbb8d30a8fcf
ms.sourcegitcommit: d6828e7422c8d74ec1e99146fedf0a05f757245f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "80395347"
---
# <a name="sendandreceivereply-template-designer"></a>SendAndReceiveReply 模板设计器
**SendAndReceiveReply**模板用于在客户端上作为请求/响应消息交换<xref:System.ServiceModel.Activities.Send>模式<xref:System.ServiceModel.Activities.ReceiveReply>的一<xref:System.Activities.Statements.Sequence>部分相关的活动中创建一对预配置的活动。

## <a name="the-sendandreceivereply-template"></a>SendAndReceiveReply 模板
 添加**SendAndReceiveReply**模板除了在<xref:System.ServiceModel.Activities.Send><xref:System.ServiceModel.Activities.ReceiveReply><xref:System.Activities.Statements.Sequence>活动中创建 和 活动之外，还执行三件事：

1. 配置 <xref:System.ServiceModel.Activities.Send.OperationName%2A> 活动的 <xref:System.ServiceModel.Activities.Send.ServiceContractName%2A> 和 <xref:System.ServiceModel.Activities.Send> 属性。

2. 将 <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A> 活动的 <xref:System.ServiceModel.Activities.ReceiveReply> 属性绑定到 <xref:System.ServiceModel.Activities.Send> 活动。

3. 创建一个 <xref:System.ServiceModel.Activities.CorrelationHandle> 作为父活动中的一个变量。

### <a name="using-the-sendandreceivereply-template-designer"></a>使用 SendAndReceiveReply 模板设计器
 **SendAndReceiveReply**活动设计器可以在**工具箱****的消息**类别中找到，该类别可通过单击"[!INCLUDE[wfd2](../includes/wfd2-md.md)]**工具箱**"选项卡进行访问（或者，从 **"视图"** 菜单中选择**工具栏**或 CTRL_ALT_X）。

 **SendAndReceiveReply**活动设计器可以从**工具箱**中拖动，并放置在[!INCLUDE[wfd2](../includes/wfd2-md.md)]通常放置活动的位置。 这将创建一<xref:System.ServiceModel.Activities.Send>个可以使用 **"发送活动"** 设计器配置的活动，以及可以使用<xref:System.ServiceModel.Activities.ReceiveReply> **ReceiveReplyForSend**设计器配置的相关活动。

 [!INCLUDE[crabout](../includes/crabout-md.md)]使用 **"发送**设计器"配置<xref:System.ServiceModel.Activities.Send>活动，请参阅["发送"](../workflow-designer/send-activity-designer.md)主题。

 [!INCLUDE[crabout](../includes/crabout-md.md)]使用**ReceiveReplyForSend**设计器配置<xref:System.ServiceModel.Activities.ReceiveReply>活动，请参阅以下部分。

### <a name="properties-of-receivereply"></a>ReceiveReply 的属性
 下表列出 <xref:System.ServiceModel.Activities.ReceiveReply> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 设计器图面上进行编辑。

|                                 属性名称                                 | 必选 |                                                                                                                                                                                                                                                                                                                                                        使用情况                                                                                                                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|               <xref:System.Activities.Activity.DisplayName%2A>                |  False   |                                                                                                                                                                                            <xref:System.ServiceModel.Activities.ReceiveReply> 活动的可选友好名称。 默认值为 ReceiveReplyForSend。<br /><br /> 虽然对友好 <xref:System.Activities.Activity.DisplayName%2A> 使用非默认值不是绝对必需的，但最好使用非默认值。                                                                                                                                                                                            |
|         <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A>         |   True   | 对与此 <xref:System.ServiceModel.Activities.Send> 活动配对的 <xref:System.ServiceModel.Activities.ReceiveReply> 活动的引用。 此属性不能**为 null**。 <xref:System.ServiceModel.Activities.Send>和<xref:System.ServiceModel.Activities.ReceiveReply>活动一起使用在客户端上建模请求/响应消息传递模式。 此属性指定配对的 <xref:System.ServiceModel.Activities.Send> 活动。 在该设计器中无法编辑此属性，因为它自动绑定到从中创建了 <xref:System.ServiceModel.Activities.Send> 活动的 <xref:System.ServiceModel.Activities.ReceiveReply> 活动。 |
|         <xref:System.ServiceModel.Activities.ReceiveReply.Content%2A>         |  False   |                        指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 通过单击属性网格中 **"内容"** 字段旁边的椭圆按钮或单击 **"定义..."** **"接收**活动设计器"表面上**的内容**标签旁边的按钮。 两者都显示 **"内容定义"** 对话框。 [!INCLUDE[crabout](../includes/crabout-md.md)]如何使用此框，请参阅[内容定义对话框主题](../workflow-designer/content-definition-dialog-box.md)。                         |
| <xref:System.ServiceModel.Activities.ReceiveReply.CorrelationInitializers%2A> |  False   |              指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Receive> 对象的集合。 单击属性网格中<xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A>属性旁边的省略号按钮以打开"**添加关联初始化器"** 对话框。 [!INCLUDE[crabout](../includes/crabout-md.md)]使用此框，请参阅[添加关联初始程序对话框主题](../workflow-designer/add-correlationinitializers-dialog-box.md)。               |
|         <xref:System.ServiceModel.Activities.ReceiveReply.Action%2A>          |  False   |                                                                                                                                                                                                                                               指定消息的操作标头。 如果未显式设置，则它的默认值为：<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}`.                                                                                                                                                                                                                                              |

## <a name="see-also"></a>另请参阅
 [关联范围](../workflow-designer/correlationscope-activity-designer.md)[初始化相关](../workflow-designer/initializecorrelation-activity-designer.md)[接收](../workflow-designer/receive-activity-designer.md)[和发送回复](../workflow-designer/receiveandsendreply-template-designer.md)[发送](../workflow-designer/send-activity-designer.md)[转接接收范围](../workflow-designer/transactedreceivescope-activity-designer.md)