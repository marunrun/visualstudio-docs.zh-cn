---
title: 工作流设计器 "初始化相关" 对话框
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InitializeCorrelation.UI
ms.assetid: 2a0a1cd3-7b9e-493e-9264-fcf85289ffcf
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d0b23f10184516ea4ffc3b00ac98e32ca8b387c1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650194"
---
# <a name="initialize-correlation-dialog-box"></a>“初始化相关”对话框

"**初始化相关**" 对话框在工作流设计器中用于编辑 <xref:System.ServiceModel.Activities.InitializeCorrelation> 活动的 <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> 属性。 有关详细信息，请参阅[InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)。

下表描述了 "**初始化相关**" 对话框的用户界面（UI）元素：

|UI 元素|描述|
|-|-----------------|
|**关联**|要初始化的相关的 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|**初始化于**|一个键/值对，包含要初始化的数据。 此值与 <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> 属性相对应。 有效的键/值对的一个示例是一个名为 "订单 Id" 的键，与一个名为 "订单 Id" 的变量配对。|

## <a name="to-launch-the-initialize-correlation-dialog-box"></a>启动“初始化相关”对话框

单击 " **InitializeCorrelation** " 活动设计器上的 "**查看**"，或在工作流设计器中选择 <xref:System.ServiceModel.Activities.InitializeCorrelation> 活动。 然后，在属性网格中单击 "<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>" 属性旁边的省略号按钮。

## <a name="see-also"></a>请参阅

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)