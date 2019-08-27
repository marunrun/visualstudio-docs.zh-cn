---
title: 工作流设计器-CorrelatesOn 定义对话框
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CorrelatesOnDefinition.UI
ms.assetid: 8b2b627a-f236-4479-aa09-525df65e3413
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d7b7336a3f3b0c2725f4e52116d0add8bf13b90e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62949809"
---
# <a name="correlateson-definition-dialog-box"></a>“CorrelatesOn 定义”对话框

**CorrelatesOn**对话框中使用工作流设计器中，若要编辑<xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A>属性的<xref:System.ServiceModel.Activities.Receive>活动。 有关详细信息，请参阅[接收活动设计器](../workflow-designer/receive-activity-designer.md)。

<xref:System.ServiceModel.Activities.Receive> 活动之间的关联指定工作流中的不同服务操作如何相互连接。

下表介绍的用户界面 (UI) 元素**CorrelatesOn**对话框。

|UI 元素|描述|
|-|-----------------|
|**CorrelatesWith**|用于将消息路由到相应工作流实例的 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|**XPath 查询**|包含用于从传入消息中提取相关数据的查询的键/值对。 此值对应于<xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A>属性。 XPath 查询包含在 <xref:System.ServiceModel.MessageQuerySet> 对象中。|

## <a name="to-launch-the-correlateson-dialog-box"></a>启动“CorrelatesOn”对话框

**接收**活动设计器可以从拖动**工具箱**和放置到工作流设计器图面，任何通常放置活动的位置。 放置在活动设计器创建<xref:System.ServiceModel.Activities.Receive>默认值的活动<xref:System.Activities.Activity.DisplayName%2A>的接收。 若要打开**CorrelatesOn 定义**对话框中，选择**接收**活动设计器，然后在属性网格中，选择的集合文本旁边的省略号按钮**CorrelatesOn**属性。

## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Activities.Receive>
- [“添加相关初始值设定项”对话框](../workflow-designer/add-correlationinitializers-dialog-box.md)
- [“初始化相关”对话框](../workflow-designer/initialize-correlation-dialog-box.md)