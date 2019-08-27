---
title: CorrelationScope 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.CorrelationScope.UI
ms.assetid: 75f20664-9042-464d-8e2b-148d365a2286
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 95c8422d53903c3c7b81db9f6ef042c5ea9ff1c1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62976764"
---
# <a name="correlationscope-activity-designer"></a>CorrelationScope 活动设计器
**CorrelationScope**活动设计器用于创建和配置<xref:System.ServiceModel.Activities.CorrelationScope>提供子消息传递活动使用的隐式管理的活动<xref:System.ServiceModel.Activities.CorrelationHandle>对象。  
  
## <a name="the-correlationscope-activity"></a>CorrelationScope 活动  
 <xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A> 属性指定用于管理子消息传递活动的 <xref:System.ServiceModel.Activities.CorrelationHandle>。 将 <xref:System.ServiceModel.Activities.Send> 中包含的 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.CorrelationScope.Body%2A> 活动配置为使用包含 <xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A> 活动的 <xref:System.ServiceModel.Activities.CorrelationScope> 属性以执行相关。  
  
### <a name="using-the-correlationscope-activity-designer"></a>使用 CorrelationScope 活动设计器  
 **CorrelationScope**活动设计器可在**消息传送**类别**工具箱**，这通过单击来访问**工具箱**选项卡的左侧[!INCLUDE[wfd2](../includes/wfd2-md.md)](或者，选择**工具栏**从**视图**菜单或 CTRL + ALT + X。)  
  
 **CorrelationScope**活动设计器可以从拖动**工具箱**拖放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面。 这将创建<xref:System.ServiceModel.Activities.CorrelationScope>默认值的活动**DisplayName** CorrelationScope。 <xref:System.Activities.Activity.DisplayName%2A>可以在的标头中编辑**CorrelationScope**活动设计器中或在**DisplayName**框**属性**窗口。  
  
 若要指定<xref:System.ServiceModel.Activities.CorrelationHandle>由子消息传递活动，单击旁边的省略号按钮**CorrelatesWith**字段中**属性**窗口中显示**表达式编辑器**对话框。 还可以在活动设计器图面上设置此属性。  
  
 范围在相关之内的活动所指定的设计器中的放置**正文**框中**CorrelationScope**设计器。  
  
### <a name="the-correlationscope-properties"></a>CorrelationScope 属性  
 下表列出 <xref:System.ServiceModel.Activities.CorrelationScope> 属性并说明如何在设计器中使用它们。 这些属性可以是中编辑**属性**窗口或在[!INCLUDE[wfd2](../includes/wfd2-md.md)]设计器图面上，并经常在这种。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.ServiceModel.Activities.InitializeCorrelation> 活动的可选友好名称。|  
|<xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A>|False|指定用于管理子消息传递活动的 <xref:System.ServiceModel.Activities.CorrelationHandle>。 如果未设置此属性，则 <xref:System.ServiceModel.Activities.CorrelationScope> 会自动创建一个隐式 <xref:System.ServiceModel.Activities.CorrelationHandle>。|  
|<xref:System.ServiceModel.Activities.CorrelationScope.Body%2A>|False|指定处于相关范围之内的活动。|  
  
## <a name="see-also"></a>请参阅  
 [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)   
 [接收](../workflow-designer/receive-activity-designer.md)   
 [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)   
 [发送](../workflow-designer/send-activity-designer.md)   
 [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)   
 [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)