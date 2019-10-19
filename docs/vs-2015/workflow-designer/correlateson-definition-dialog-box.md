---
title: "\"CorrelatesOn 定义\" 对话框 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- CorrelatesOnDefinition.UI
ms.assetid: 8b2b627a-f236-4479-aa09-525df65e3413
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e2a9a6f7ec6b8bf246ebfc03c166780b229e1aee
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656940"
---
# <a name="correlateson-definition-dialog-box"></a>“CorrelatesOn 定义”对话框
在 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 中使用 " **CorrelatesOn** " 对话框编辑 <xref:System.ServiceModel.Activities.Receive> 活动的 <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> 属性。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][接收](../workflow-designer/receive-activity-designer.md)主题。

 <xref:System.ServiceModel.Activities.Receive> 活动之间的关联指定工作流中的不同服务操作如何相互连接。

 下表介绍了 " **CorrelatesOn** " 对话框的用户界面（UI）元素。

|UI 元素|描述|
|----------------|-----------------|
|**CorrelatesWith**|用于将消息路由到相应工作流实例的 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|**XPath 查询**|包含用于从传入消息中提取相关数据的查询的键/值对。 它对应于 <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> 属性。 XPath 查询包含在 <xref:System.ServiceModel.MessageQuerySet> 对象中。|

## <a name="to-launch-the-correlateson-dialog-box"></a>启动“CorrelatesOn”对话框
 可以将 "**接收**" 活动设计器从 "**工具箱**" 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置。 这将创建具有 Receive 的默认 <xref:System.ServiceModel.Activities.Receive> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 选择 "**接收**" 活动设计器，然后在属性网格中单击 " **CorrelatesOn** " 属性的 "（集合）" 文本旁的省略号按钮，以显示 " **CorrelatesOn 定义**" 对话框。

## <a name="see-also"></a>请参阅
 <xref:System.ServiceModel.Activities.Receive> ["添加 CorrelationInitializers" 对话框中的 "](../workflow-designer/add-correlationinitializers-dialog-box.md) [初始化相关](../workflow-designer/initialize-correlation-dialog-box.md)" 对话框