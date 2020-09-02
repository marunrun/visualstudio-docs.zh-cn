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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656940"
---
# <a name="correlateson-definition-dialog-box"></a>“CorrelatesOn 定义”对话框
**CorrelatesOn**对话框用于 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 编辑 <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> 活动的属性 <xref:System.ServiceModel.Activities.Receive> 。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][接收](../workflow-designer/receive-activity-designer.md)主题。

 <xref:System.ServiceModel.Activities.Receive> 活动之间的关联指定工作流中的不同服务操作如何相互连接。

 下表介绍了 " **CorrelatesOn** " 对话框 (UI) 元素的用户界面。

|UI 元素|说明|
|----------------|-----------------|
|**CorrelatesWith**|用于将消息路由到相应工作流实例的 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|**XPath 查询**|包含用于从传入消息中提取相关数据的查询的键/值对。 它对应于 <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> 属性。 XPath 查询包含在 <xref:System.ServiceModel.MessageQuerySet> 对象中。|

## <a name="to-launch-the-correlateson-dialog-box"></a>启动“CorrelatesOn”对话框
 可以将 " **接收** " 活动设计器从 " **工具箱** " 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置。 这将创建具有 Receive 的默认 <xref:System.ServiceModel.Activities.Receive> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 选择 "**接收**" 活动设计器，然后单击 " (集合" 旁边的省略号按钮) " **CorrelatesOn 定义**" 对话框的 "属性" 网格中的 " **CorrelatesOn** " 属性的文本。

## <a name="see-also"></a>另请参阅
 <xref:System.ServiceModel.Activities.Receive>["添加 CorrelationInitializers" 对话框 "](../workflow-designer/add-correlationinitializers-dialog-box.md) [初始化相关" 对话框](../workflow-designer/initialize-correlation-dialog-box.md)