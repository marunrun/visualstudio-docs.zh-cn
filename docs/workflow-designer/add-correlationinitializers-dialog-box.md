---
title: "\"添加 CorrelationInitializers\" 对话框"
description: 了解如何使用工作流设计器中的 "添加相关初始值设定项" 对话框来配置发送、接收和 SendReply 活动的 CorrelationInitializers 属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AddCorrelationInitializers.UI
ms.assetid: c0517467-d54a-4ee6-aef0-c19b96b6f395
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0e5822d1dc79835dd6fdcc3a70c3392dbd3d1aab
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96996352"
---
# <a name="add-correlationinitializers-dialog-box"></a>“添加相关初始值设定项”对话框

在工作流设计器中使用 "**添加相关初始值设定项**" 对话框来配置 <xref:System.ServiceModel.Activities.Send> 、 <xref:System.ServiceModel.Activities.Receive> 、 <xref:System.ServiceModel.Activities.SendReply> 和活动的 CorrelationInitializers 属性 <xref:System.ServiceModel.Activities.ReceiveReply> 。 有关使用此框的活动设计器的详细信息，请参阅 [Send](../workflow-designer/send-activity-designer.md)、 [Receive](../workflow-designer/receive-activity-designer.md)、 [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)和 [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md) 主题。

此对话框指定的集合中的相关初始值设定项可以初始化消息传递活动之间的下列关联：

- 基于查询
- 上下文
- 回调上下文
- 请求-答复

下表介绍了 " **添加相关初始值设定项** " 对话框的用户界面 (UI) 元素：

|UI 元素|说明|
|-|-----------------|
|**添加初始值设定项**|单击 " **添加初始化** " 框，将附加的初始值设定项添加到集合中。|
|**相关类型**|指定相关初始值设定项的类型。 有四种类型可供选择：<br /><br /> 1. 用于指定的回调相关初始值设定项 <xref:System.ServiceModel.Activities.CallbackCorrelationInitializer> 。<br />2. 用于指定的上下文相关初始值设定项 <xref:System.ServiceModel.Activities.CorrelationInitializer> 。<br />3. 用于指定的请求-答复相关初始值设定项 <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> 。<br />4. 用于指定的查询相关初始值设定项 <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 。<br /><br /> 编辑 **CorrelationType**<br /><br /> 1. 将选项卡 **添加到添加初始值设定项** DataGrid 中的特定行。<br />2. 若要将焦点设置到 **CorrelationTypeComboBox**，请按 **Ctrl** + **tab**。<br />3. 按 Alt + 向下键可弹出 **组合框** 并对其进行编辑。|
|**XPath 查询**|包含用于从传入和传出消息中提取相关数据的查询的键/值对。 仅当使用 <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 类型时此列表才有效。|

## <a name="to-launch-the-add-correlation-initializers-dialog-box"></a>启动“添加相关初始值设定项”对话框

 " **添加相关初始值设定项** " 对话框由 **发送**、 **接收**、 **ReceiveAndSendReply** 和 **SendAndReceiveReply** 设计器使用。 在每种情况下，访问它们的方式都类似，这里使用的是 **接收** 设计器的事例阐释了该过程。

 可以将 " **接收** " 活动设计器从 " **工具箱** " 拖放到工作流设计器图面上放置活动的任何位置。 删除 **receive** 活动设计器将创建一个 <xref:System.ServiceModel.Activities.Receive> 活动，其中默认为 <xref:System.Activities.Activity.DisplayName%2A> receive。 选择 "**接收**" 活动设计器，然后单击 " (集合" 旁边的省略号按钮，将显示 "**添加相关初始值设定项**" 对话框的 "属性" 网格中的 " **CorrelationInitializers** " 属性) 文本。

## <a name="see-also"></a>另请参阅

- [“初始化相关”对话框](../workflow-designer/initialize-correlation-dialog-box.md)
