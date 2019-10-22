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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 145b67574169696771f4102b29e9dc8f6a9d1575
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659024"
---
# <a name="initializecorrelation-activity-designer"></a>InitializeCorrelation 活动设计器
" **InitializeCorrelation** " 活动设计器用于创建和配置一个 <xref:System.ServiceModel.Activities.InitializeCorrelation> 活动，该活动用于在发送或接收消息之前在消息间建立关联。

## <a name="the-initializecorrelation-activity"></a>InitializeCorrelation 活动
 <xref:System.ServiceModel.Activities.InitializeCorrelation> 活动用于在不发送或接收消息的情况下初始化相关。 通常，相关是在发送或接收消息时初始化的。 如果必须在发送或接收消息前建立相关，请使用 <xref:System.ServiceModel.Activities.InitializeCorrelation> 来初始化该相关。

### <a name="using-the-initializecorrelation-activity-designer"></a>使用 InitializeCorrelation 活动设计器
 " **InitializeCorrelation** " 活动设计器可在 "**工具箱**" 的 "**消息传送**" 类别中找到，可通过单击 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 上的 "**工具箱**" 选项卡（或者，从视图中选择 "**工具栏**"菜单或 CTRL + ALT + X。）

 可以将 " **InitializeCorrelation** " 活动设计器从 "**工具箱**" 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上。 这将创建一个 <xref:System.ServiceModel.Activities.InitializeCorrelation> 的默认 <xref:System.Activities.Activity.DisplayName%2A> 为 InitializeCorrelation 的活动。 <xref:System.Activities.Activity.DisplayName%2A> 可以在 " **InitializeCorrelation** " 活动设计器的标头中或在 "**属性**" 窗口的 " **DisplayName** " 框中进行编辑。

 可以在 " **InitializeCorrelation** " 活动设计器图面上的 "**属性**" 窗口中的 "**相关**" 字段中指定 <xref:System.ServiceModel.Activities.CorrelationHandle>。

 单击 "**属性**" 窗口中的 " **CorrelationData** " 字段旁边的省略号按钮，或单击 "查看 ..." **InitializeCorrelation**活动设计器图面上的提示文本显示 "**初始化相关**" 对话框，在该对话框中可以指定相关句柄和用于初始化它的键值对。 使用此对话框 [!INCLUDE[crabout](../includes/crabout-md.md)]，请参阅 "[类型集合编辑器" 对话框](../workflow-designer/type-collection-editor-dialog-box.md)主题。

### <a name="the-initializecorrelation-properties"></a>InitializeCorrelation 属性
 下表列出 <xref:System.ServiceModel.Activities.InitializeCorrelation> 属性并说明如何在设计器中使用它们。 这些属性可以在 "**属性**" 窗口中或 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上进行编辑。

|属性名|必需|用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.ServiceModel.Activities.InitializeCorrelation> 活动的友好名称。 默认值为 InitializeCorrelation。<br /><br /> 虽然对友好 <xref:System.Activities.Activity.DisplayName%2A> 使用非默认值不是绝对必需的，但最好使用非默认值。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.Correlation%2A>|False|用于关联相关中的工作流活动的 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>|False|将消息与工作流实例相关联的相关数据的字典。<br /><br /> 使用 "**初始化相关**" 对话框配置 <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>。 [!INCLUDE[crabout](../includes/crabout-md.md)] "使用此对话框，请参阅"[类型集合编辑器 "对话框](../workflow-designer/type-collection-editor-dialog-box.md)主题。|

## <a name="see-also"></a>请参阅
 [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md) [Receive](../workflow-designer/receive-activity-designer.md) [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md) [Send](../workflow-designer/send-activity-designer.md) [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md) [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)