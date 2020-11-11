---
title: "\"工作流设计器-内容定义\" 对话框"
description: 了解如何使用 "内容定义" 对话框配置发送、接收、SendReply 和 ReceiveReply 活动的内容属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MessageContent.UI
ms.assetid: 7e4237c3-90a1-4149-bd8a-3643d1dde0df
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2858c179d05645b3e47e6be27e386168392fcb48
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94438160"
---
# <a name="content-definition-dialog-box"></a>“内容定义”对话框

" **内容定义** " 对话框在工作流设计器中用于配置 **Content** <xref:System.ServiceModel.Activities.Send> 、 <xref:System.ServiceModel.Activities.Receive> 、 <xref:System.ServiceModel.Activities.SendReply> 和活动的内容属性 <xref:System.ServiceModel.Activities.ReceiveReply> 。 有关使用此框的活动设计器的详细信息，请参阅 [Send](../workflow-designer/send-activity-designer.md)、 [Receive](../workflow-designer/receive-activity-designer.md)、 [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)和 [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md) 主题。

下表描述了 " **初始化相关** " 对话框 (UI) 元素的用户界面：

|UI 元素|说明|
|-|-----------------|
|**Message**|使用 " **消息数据** 表达式" 文本框和 " **消息类型** " 下拉列表框指定类型的消息内容。 默认情况下， **内容定义** 使用 <xref:System.ServiceModel.Activities.ReceiveMessageContent> ，它需要 <xref:System.ServiceModel.Channels.Message> 工作流服务定义中的或消息协定类型。|
|**Parameters**|单击 " **参数** " 单选按钮以使用 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 需要数据协定的。 使用数据网格设置 <xref:System.Activities.OutArgument> 键/值对的泛型集合，这些键/值对的值将赋给当前工作流中的可变参数。|

" **内容定义** " 对话框由 " **Send** "、" **Receive** "、" **ReceiveAndSendReply** " 和 " **SendAndReceiveReply** " 设计器使用。 在任何情况下访问它们的方式都相同，此处使用“Receive”设计器来演示该过程。

可以将 " **接收** " 活动设计器从 " **工具箱** " 拖放到工作流设计器图面上通常放置活动的任何位置。 这将创建具有 Receive 的默认 <xref:System.ServiceModel.Activities.Receive> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 选择 " **接收** " 活动设计器，然后单击 "内容 **定义** " 对话框的 "属性" 网格中 " **内容** " 属性旁边的省略号按钮 (内容 ") 文本。

可以在活动的 **消息** 部分 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 或活动的 **参数** 部分中指定内容 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 。

## <a name="see-also"></a>另请参阅

- [工作流设计器 UI 帮助](browse-and-select-a-dotnet-type-dialog-box.md)