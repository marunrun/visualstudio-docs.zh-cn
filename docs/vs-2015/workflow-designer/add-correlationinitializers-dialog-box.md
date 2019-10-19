---
title: "\"添加 CorrelationInitializers\" 对话框 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- AddCorrelationInitializers.UI
ms.assetid: c0517467-d54a-4ee6-aef0-c19b96b6f395
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e1402b90dfc78068546b510ce6b85379b1695f47
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672040"
---
# <a name="add-correlationinitializers-dialog-box"></a>“添加相关初始值设定项”对话框
在 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 中使用 "**添加相关初始值设定项**" 对话框来配置 <xref:System.ServiceModel.Activities.Send>、<xref:System.ServiceModel.Activities.Receive>、<xref:System.ServiceModel.Activities.SendReply> 和 <xref:System.ServiceModel.Activities.ReceiveReply> 活动的**CorrelationInitializers**属性。 [!INCLUDE[crabout](../includes/crabout-md.md)] 使用此框的活动设计器，请参阅[Send](../workflow-designer/send-activity-designer.md)、 [Receive](../workflow-designer/receive-activity-designer.md)、 [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)和[SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)主题。

 使用此对话框指定的集合中的相关初始值设定项可初始化基于查询的上下文、回调上下文或各消息传递活动之间的请求-答复相关性。

 下表描述了 "**添加相关初始值设定项**" 对话框的用户界面（UI）元素。

|UI 元素|描述|
|----------------|-----------------|
|**添加初始值设定项**|单击 "**添加初始化**" 框，将附加的初始值设定项添加到集合中。|
|**相关类型**|指定相关初始值设定项的类型。 有四种类型可供选择：<br /><br /> 1. 用于指定 <xref:System.ServiceModel.Activities.CallbackCorrelationInitializer> 的回调相关初始值设定项。<br />2. 用于指定 <xref:System.ServiceModel.Activities.CorrelationInitializer> 的上下文相关初始值设定项。<br />3. 用于指定 <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> 的请求-答复相关初始值设定项。<br />4. 用于指定 <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 的查询相关初始值设定项。<br /><br /> 编辑**CorrelationType**<br /><br /> 1. 将选项卡**添加到添加初始值设定项**DataGrid 中的特定行。<br />2. 按 Ctrl + Tab 将焦点设置到**CorrelationTypeComboBox**<br />3. 按 Alt + 向下键可弹出**组合框**并对其进行编辑。|
|**XPath 查询**|包含用于从传入和传出消息中提取相关数据的查询的键/值对。 仅当使用 <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 类型时此列表才有效。|

## <a name="to-launch-the-add-correlation-initializers-dialog-box"></a>启动“添加相关初始值设定项”对话框
 "**添加相关初始值设定项**" 对话框由**发送**、**接收**、 **ReceiveAndSendReply**和**SendAndReceiveReply**设计器使用。 在这两种情况下，访问它们的方式类似，其中使用**接收**设计器的情况说明了该过程。

 可以将 "**接收**" 活动设计器从 "**工具箱**" 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置。 这将创建具有 Receive 的默认 <xref:System.ServiceModel.Activities.Receive> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 选择 "**接收**" 活动设计器，然后在属性网格中单击 " **CorrelationInitializers** " 属性的 "（集合）" 文本旁的省略号按钮，以显示 "**添加相关初始值设定项**" 对话框。

## <a name="see-also"></a>请参阅
 [“初始化相关”对话框](../workflow-designer/initialize-correlation-dialog-box.md)