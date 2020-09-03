---
title: 工作流设计器 "初始化相关" 对话框
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InitializeCorrelation.UI
ms.assetid: 2a0a1cd3-7b9e-493e-9264-fcf85289ffcf
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 04f0a3bb70dbab31e0faa5c38caac9b54c6154fe
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "76114778"
---
# <a name="initialize-correlation-dialog-box"></a>“初始化相关”对话框

" **初始化相关** " 对话框在工作流设计器中用于编辑活动的 <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> 属性 <xref:System.ServiceModel.Activities.InitializeCorrelation> 。 有关详细信息，请参阅 [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)。

下表描述了 " **初始化相关** " 对话框 (UI) 元素的用户界面：

|UI 元素|说明|
|-|-----------------|
|**Correlation (相关性)** |要初始化的相关的 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|**初始化开**|一个键/值对，包含要初始化的数据。 此值与属性相对应 <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> 。 有效的键/值对的一个示例是一个名为 "订单 Id" 的键，与一个名为 "订单 Id" 的变量配对。|

## <a name="to-launch-the-initialize-correlation-dialog-box"></a>启动“初始化相关”对话框

单击 " **InitializeCorrelation** " 活动设计器上的 "**查看**"，或 <xref:System.ServiceModel.Activities.InitializeCorrelation> 在工作流设计器中选择一个活动。 然后，在属性网格中单击属性旁的省略号按钮 <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> 。

## <a name="see-also"></a>另请参阅

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
