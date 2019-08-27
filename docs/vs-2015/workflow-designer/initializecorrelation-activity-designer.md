---
title: InitializeCorrelation 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.InitializeCorrelation.UI
ms.assetid: 4c54f34c-ee84-42a6-abb0-ec260c1ccb76
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 383a2e892c8f0962ab8c09d5e8984d3cc570ebaa
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62979977"
---
# <a name="initializecorrelation-activity-designer"></a>InitializeCorrelation 活动设计器
**InitializeCorrelation**活动设计器用于创建和配置<xref:System.ServiceModel.Activities.InitializeCorrelation>用于消息之前发送或接收这些消息之间建立相关的活动。  
  
## <a name="the-initializecorrelation-activity"></a>InitializeCorrelation 活动  
 <xref:System.ServiceModel.Activities.InitializeCorrelation> 活动用于在不发送或接收消息的情况下初始化相关。 通常，相关是在发送或接收消息时初始化的。 如果必须在发送或接收消息前建立相关，请使用 <xref:System.ServiceModel.Activities.InitializeCorrelation> 来初始化该相关。  
  
### <a name="using-the-initializecorrelation-activity-designer"></a>使用 InitializeCorrelation 活动设计器  
 **InitializeCorrelation**活动设计器可在**消息传送**类别**工具箱**，这通过单击来访问**工具箱**选项卡上[!INCLUDE[wfd2](../includes/wfd2-md.md)](或者，选择**工具栏**从**视图**菜单或 CTRL + ALT + X。)  
  
 **InitializeCorrelation**活动设计器可以从拖动**工具箱**拖放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面。 这将创建<xref:System.ServiceModel.Activities.InitializeCorrelation>默认值的活动<xref:System.Activities.Activity.DisplayName%2A>的 InitializeCorrelation.The<xref:System.Activities.Activity.DisplayName%2A>可以在的标头中编辑**InitializeCorrelation**活动设计器中或在**DisplayName**的框**属性**窗口。  
  
 <xref:System.ServiceModel.Activities.CorrelationHandle>可以是在指定**相关**字段中**属性**上的窗口**InitializeCorrelation**活动设计器图面。  
  
 单击省略号按钮，除了**CorrelationData**字段中**属性**窗口或"查看..." 在提示文字**InitializeCorrelation**活动设计器图面显示**初始化相关**对话框可以在其中指定相关句柄和用于对键 / 值对对其进行初始化。 [!INCLUDE[crabout](../includes/crabout-md.md)] 使用此对话框中，请参阅[类型集合编辑器对话框](../workflow-designer/type-collection-editor-dialog-box.md)主题。  
  
### <a name="the-initializecorrelation-properties"></a>InitializeCorrelation 属性  
 下表列出 <xref:System.ServiceModel.Activities.InitializeCorrelation> 属性并说明如何在设计器中使用它们。 这些属性可以在中编辑**属性**窗口或在[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.ServiceModel.Activities.InitializeCorrelation> 活动的友好名称。 默认值为 InitializeCorrelation。<br /><br /> 虽然对友好 <xref:System.Activities.Activity.DisplayName%2A> 使用非默认值不是绝对必需的，但最好使用非默认值。|  
|<xref:System.ServiceModel.Activities.InitializeCorrelation.Correlation%2A>|False|用于关联相关中的工作流活动的 <xref:System.ServiceModel.Activities.CorrelationHandle>。|  
|<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>|False|将消息与工作流实例相关联的相关数据的字典。<br /><br /> 使用**初始化相关**对话框可以配置<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>。 [!INCLUDE[crabout](../includes/crabout-md.md)] 使用此对话框中，请参阅[类型集合编辑器对话框](../workflow-designer/type-collection-editor-dialog-box.md)主题。|  
  
## <a name="see-also"></a>请参阅  
 [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)   
 [接收](../workflow-designer/receive-activity-designer.md)   
 [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)   
 [发送](../workflow-designer/send-activity-designer.md)   
 [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)   
 [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)