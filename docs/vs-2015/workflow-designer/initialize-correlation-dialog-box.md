---
title: "\"初始化相关\" 对话框 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- InitializeCorrelation.UI
ms.assetid: 2a0a1cd3-7b9e-493e-9264-fcf85289ffcf
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3ab913027a6a992494dad609b98ab11dbc6ae61c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659043"
---
# <a name="initialize-correlation-dialog-box"></a>“初始化相关”对话框
"**初始化相关**" 对话框在 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 中用于编辑 <xref:System.ServiceModel.Activities.InitializeCorrelation> 活动的 <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> 属性。 [!INCLUDE[crdefault](../includes/crdefault-md.md)] [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)主题。

 下表描述了 "**初始化相关**" 对话框的用户界面（UI）元素。

|UI 元素|描述|
|----------------|-----------------|
|**关联**|要初始化的相关的 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|**初始化于**|一个键/值对，包含要初始化的数据。 它对应于 <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> 属性。 有效键/值对的一个示例是名为“OrderID”的键与名为 OrderID 的变量配对。|

## <a name="to-launch-the-initialize-correlation-dialog-box"></a>启动“初始化相关”对话框

- 单击 " **InitializeCorrelation** " 活动设计器上的 "**查看**"，或在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 中选择 <xref:System.ServiceModel.Activities.InitializeCorrelation> 活动，然后在属性网格中单击 "<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>" 属性旁边的省略号按钮。

## <a name="see-also"></a>请参阅
 [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)