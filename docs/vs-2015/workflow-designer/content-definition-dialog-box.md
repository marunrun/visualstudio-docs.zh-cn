---
title: "\"内容定义\" 对话框 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- MessageContent.UI
ms.assetid: 7e4237c3-90a1-4149-bd8a-3643d1dde0df
caps.latest.revision: 3
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d989f5a0c57e381041e8fe9c200aae1a76316ad8
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656948"
---
# <a name="content-definition-dialog-box"></a>“内容定义”对话框
"**内容定义**" 对话框用于 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 配置 <xref:System.ServiceModel.Activities.Send>、<xref:System.ServiceModel.Activities.Receive>、<xref:System.ServiceModel.Activities.SendReply> 和 <xref:System.ServiceModel.Activities.ReceiveReply> 活动的**内容**属性。 [!INCLUDE[crabout](../includes/crabout-md.md)] 使用此框的活动设计器，请参阅[Send](../workflow-designer/send-activity-designer.md)、 [Receive](../workflow-designer/receive-activity-designer.md)、 [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)和[SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)主题。

 下表描述了 "**初始化相关**" 对话框的用户界面（UI）元素。

|UI 元素|描述|
|----------------|-----------------|
|**消息**|使用 "**消息数据**表达式" 文本框和 "**消息类型**" 下拉列表框指定类型的消息内容。 默认情况下，**内容定义**使用 <xref:System.ServiceModel.Activities.ReceiveMessageContent>，这需要在工作流服务定义中使用 <xref:System.ServiceModel.Channels.Message> 或消息协定类型。|
|**参数**|单击 "**参数**" 单选按钮以使用需要数据协定 <xref:System.ServiceModel.Activities.ReceiveParametersContent>。 使用数据网格设置 <xref:System.Activities.OutArgument> 键/值对的泛型集合，这些键/值对的值将赋给当前工作流中的可变参数。|

 "**内容定义**" 对话框由 " **Send**"、" **Receive**"、" **ReceiveAndSendReply**" 和 " **SendAndReceiveReply** " 设计器使用。 在任何情况下访问它们的方式都相同，此处使用“Receive”设计器来演示该过程。

 可以将 "**接收**" 活动设计器从 "**工具箱**" 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置。 这将创建具有 Receive 的默认 <xref:System.ServiceModel.Activities.Receive> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 选择 "**接收**" 活动设计器，然后单击 "内容定义" 对话框的 **"内容" 属性的**"（内容）" 文本旁的省略号按钮，以显示 "**内容定义**" 对话框。

 可以在 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动的**消息**部分中或在 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动的**参数**部分中指定内容。

## <a name="see-also"></a>请参阅
 [工作流设计器 UI 帮助](../workflow-designer/workflow-designer-ui-help.md)