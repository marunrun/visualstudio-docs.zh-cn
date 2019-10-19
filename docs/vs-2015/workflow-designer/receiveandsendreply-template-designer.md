---
title: ReceiveAndSendReply 模板设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.ReceiveAndSendReply.UI
- System.ServiceModel.Activities.SendReply.UI
ms.assetid: d1d9a058-df7e-48f5-a2e7-3caeeba7eaa6
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e853967f73c99aa52958754e9f59f644c2f9497b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672544"
---
# <a name="receiveandsendreply-template-designer"></a>ReceiveAndSendReply 模板设计器
**ReceiveAndSendReply**模板用于在 <xref:System.Activities.Statements.Sequence> 活动中创建一对预配置的 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动，并将其与服务器上的请求/响应消息交换模式的一部分相关联。

## <a name="the-receiveandsendreply-template"></a>ReceiveAndSendReply 模板
 添加**ReceiveAndSendReply**模板除了创建 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动 <xref:System.Activities.Statements.Sequence> 活动外，还执行三个操作：

1. 配置 <xref:System.ServiceModel.Activities.Receive.OperationName%2A> 活动的 <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> 和 <xref:System.ServiceModel.Activities.Receive> 属性。

2. 将 <xref:System.ServiceModel.Activities.SendReply.Request%2A> 活动的 <xref:System.ServiceModel.Activities.Receive> 属性绑定到 <xref:System.ServiceModel.Activities.Send> 活动。

3. 创建一个 <xref:System.ServiceModel.Activities.CorrelationHandle> 作为父活动中的一个变量。

### <a name="using-the-receiveandsendreply-template-designer"></a>使用 ReceiveAndSendReply 模板设计器
 " **ReceiveAndSendReply** " 活动设计器可在 "**工具箱**" 的 "**消息传送**" 类别中找到，可通过单击 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 中的 "**工具箱**" 选项卡（或者，从**视图**中选择 "**工具栏**" 来访问）。菜单，或按 CTRL + ALT + X。）

 可以将 " **ReceiveAndSendReply** " 活动设计器从 "**工具箱**" 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置。 这将创建一个 <xref:System.ServiceModel.Activities.Receive> 活动，该活动可使用 "**发送**活动设计器" 和一个可使用 SendReplyToReceive 设计器配置的相关 <xref:System.ServiceModel.Activities.SendReply> 进行配置。

 [!INCLUDE[crabout](../includes/crabout-md.md)] 使用**接收**设计器配置 <xref:System.ServiceModel.Activities.Receive> 活动，请参阅[接收](../workflow-designer/receive-activity-designer.md)主题。

 [!INCLUDE[crabout](../includes/crabout-md.md)] 使用**SendReplyToReceive**设计器配置 <xref:System.ServiceModel.Activities.SendReply> 活动，请参阅下一节。

### <a name="properties-of-sendreply"></a>SendReply 的属性
 下表列出 <xref:System.ServiceModel.Activities.SendReply> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 设计器图面上进行编辑。

|                               属性名                                | 必需 |                                                                                                                                                                                                                                                                                                                                                      用法                                                                                                                                                                                                                                                                                                                                                       |
|----------------------------------------------------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              <xref:System.Activities.Activity.DisplayName%2A>              |  False   |                                                                                                                                                                                            <xref:System.ServiceModel.Activities.SendReply> 活动的可选友好名称。 默认值为 SendReplyToReceive。<br /><br /> 虽然对友好 <xref:System.Activities.Activity.DisplayName%2A> 使用非默认值不是绝对必需的，但最好使用非默认值。                                                                                                                                                                                             |
|         <xref:System.ServiceModel.Activities.SendReply.Request%2A>         |   True   | 对与此 <xref:System.ServiceModel.Activities.Receive> 活动配对的 <xref:System.ServiceModel.Activities.SendReply> 活动的引用。 此属性不能为**null**。 在服务器上将 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动配合使用，可对请求/响应消息模式进行建模。 此属性指定配对的 <xref:System.ServiceModel.Activities.Send> 活动。 在该设计器中无法编辑此属性，因为它自动绑定到从中创建了 <xref:System.ServiceModel.Activities.Send> 活动的 <xref:System.ServiceModel.Activities.SendReply> 活动。 |
|         <xref:System.ServiceModel.Activities.SendReply.Content%2A>         |  False   |                       指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 编辑此属性，方法是单击属性网格中 "**内容**" 字段旁边的省略号按钮，或单击 "**定义 ...** " "**接收**" 活动设计器图面上的 "**内容**" 标签旁边的按钮。 两者都显示 "**内容定义**" 对话框。 [!INCLUDE[crabout](../includes/crabout-md.md)] 如何使用此框，请参阅 "[内容定义" 对话框](../workflow-designer/content-definition-dialog-box.md)主题。                       |
| <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> |  False   |            指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Receive> 对象的集合。 单击 "属性" 网格中 "<xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A>" 属性旁边的省略号按钮，以打开 "**添加相关初始值设定项**" 对话框。 [!INCLUDE[crabout](../includes/crabout-md.md)] 使用此框，请参阅[Add CorrelationInitializers 对话框](../workflow-designer/add-correlationinitializers-dialog-box.md)主题。            |
|         <xref:System.ServiceModel.Activities.SendReply.Action%2A>          |  False   |                                                                                                                                                                                                                                              指定消息的操作标头。 如果未显式设置，则它的默认值为：<br /><br /> <strong>https://tempuri.org/{service 协定命名空间}/协定名称}/{操作名称}</strong>                                                                                                                                                                                                                                              |
|    <xref:System.ServiceModel.Activities.SendReply.PersistBeforeSend%2A>    |  False   |                                                                                                                                                                                                                                                                                          指定在发送回复消息前是否应保留工作流实例。 默认值为“false”。                                                                                                                                                                                                                                                                                           |

## <a name="see-also"></a>请参阅
 [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md) [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md) [Receive](../workflow-designer/receive-activity-designer.md) [Send](../workflow-designer/send-activity-designer.md) [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md) [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)