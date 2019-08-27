---
title: 工作流设计器-添加相关初始值设定项对话框
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AddCorrelationInitializers.UI
ms.assetid: c0517467-d54a-4ee6-aef0-c19b96b6f395
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 21c030295d325ea1ee4d546356f8cda5ef6ffd3f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62946646"
---
# <a name="add-correlationinitializers-dialog-box"></a>“添加相关初始值设定项”对话框

**添加相关初始值设定项**对话框中使用工作流设计器中，若要配置**相关初始值设定项**的属性<xref:System.ServiceModel.Activities.Send>， <xref:System.ServiceModel.Activities.Receive>， <xref:System.ServiceModel.Activities.SendReply>，和<xref:System.ServiceModel.Activities.ReceiveReply>活动。 有关使用此框的活动设计器的详细信息，请参阅[发送](../workflow-designer/send-activity-designer.md)，[接收](../workflow-designer/receive-activity-designer.md)， [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)，和[SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)主题。

使用此对话框中指定的集合中的相关初始值设定项可以初始化间消息传递活动的以下关联：

- 基于查询的
- Context — 上下文
- 回调上下文
- request-reply

下表介绍的用户界面 (UI) 元素**添加相关初始值设定项**对话框：

|UI 元素|描述|
|-|-----------------|
|**添加初始值设定项**|单击**添加 initialize**框以将其他初始值设定项添加到集合。|
|**相关类型**|指定相关初始值设定项的类型。 有四种类型可供选择：<br /><br /> 1.用于指定 <xref:System.ServiceModel.Activities.CallbackCorrelationInitializer> 的回调相关初始值设定项。<br />2.用于指定 <xref:System.ServiceModel.Activities.CorrelationInitializer> 的上下文相关初始值设定项。<br />3.用于指定 <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> 的请求-答复相关初始值设定项。<br />4.用于指定 <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 的查询相关初始值设定项。<br /><br /> 若要编辑**CorrelationType**<br /><br /> 1.中的特定行的选项卡**添加初始值设定项**DataGrid。<br />2.若要将焦点设置到**CorrelationTypeComboBox**，按**Ctrl**+**选项卡**。<br />3.按 Alt + 向下弹出**组合框**和对其进行编辑。|
|**XPath 查询**|包含用于从传入和传出消息中提取相关数据的查询的键/值对。 仅当使用 <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 类型时此列表才有效。|

## <a name="to-launch-the-add-correlation-initializers-dialog-box"></a>启动“添加相关初始值设定项”对话框

 **添加相关初始值设定项**通过使用对话框**发送**，**接收**， **ReceiveAndSendReply**，和**SendAndReceiveReply**设计器。 访问它们是在每种情况下，并涉及到这种情况类似**接收**此处使用设计器来演示该过程。

 **接收**活动设计器可以从拖动**工具箱**和任何放置活动的位置放置到工作流设计器图面。 删除**接收**活动设计器创建<xref:System.ServiceModel.Activities.Receive>默认值的活动<xref:System.Activities.Activity.DisplayName%2A>的接收。 选择**接收**活动设计器并单击 （集合） 文本旁的省略号按钮**相关初始值设定项**属性在属性网格中的**添加相关初始值设定项**对话框出现。

## <a name="see-also"></a>请参阅

- [“初始化相关”对话框](../workflow-designer/initialize-correlation-dialog-box.md)