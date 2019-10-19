---
title: "\"工作流设计器 CorrelatesOn 定义\" 对话框"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CorrelatesOnDefinition.UI
ms.assetid: 8b2b627a-f236-4479-aa09-525df65e3413
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 401f72f55f23779f7c6257437034a4ebc294d219
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650602"
---
# <a name="correlateson-definition-dialog-box"></a>“CorrelatesOn 定义”对话框

在工作流设计器中使用 " **CorrelatesOn** " 对话框编辑 <xref:System.ServiceModel.Activities.Receive> 活动的 <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> 属性。 有关详细信息，请参阅[Receive 活动设计器](../workflow-designer/receive-activity-designer.md)。

<xref:System.ServiceModel.Activities.Receive> 活动之间的关联指定工作流中的不同服务操作如何相互连接。

下表介绍了 " **CorrelatesOn** " 对话框的用户界面（UI）元素。

|UI 元素|描述|
|-|-----------------|
|**CorrelatesWith**|用于将消息路由到相应工作流实例的 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|**XPath 查询**|包含用于从传入消息中提取相关数据的查询的键/值对。 此值与 <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> 属性相对应。 XPath 查询包含在 <xref:System.ServiceModel.MessageQuerySet> 对象中。|

## <a name="to-launch-the-correlateson-dialog-box"></a>启动“CorrelatesOn”对话框

可以将 "**接收**" 活动设计器从 **"工具箱**" 拖放到工作流设计器图面上通常放置活动的任何位置。 删除活动设计器将创建一个 <xref:System.ServiceModel.Activities.Receive> 的活动，其中包含默认的接收 <xref:System.Activities.Activity.DisplayName%2A>。 若要打开 " **CorrelatesOn 定义**" 对话框，请选择 "**接收**" 活动设计器，然后在属性网格中，选择**CorrelatesOn**属性的集合文本旁边的省略号按钮。

## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Activities.Receive>
- [“添加相关初始值设定项”对话框](../workflow-designer/add-correlationinitializers-dialog-box.md)
- [“初始化相关”对话框](../workflow-designer/initialize-correlation-dialog-box.md)