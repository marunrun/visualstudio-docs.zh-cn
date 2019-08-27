---
title: 工作流设计器-InitializeCorrelation 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.InitializeCorrelation.UI
ms.assetid: 4c54f34c-ee84-42a6-abb0-ec260c1ccb76
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 496aefb2679edd87c892c54f44b14876b4ebce5b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62536434"
---
# <a name="initializecorrelation-activity-designer"></a>InitializeCorrelation 活动设计器

**InitializeCorrelation**活动设计器用于创建和配置<xref:System.ServiceModel.Activities.InitializeCorrelation>活动。 <xref:System.ServiceModel.Activities.InitializeCorrelation>活动建立之前发送或接收这些消息之间的相关性。

## <a name="the-initializecorrelation-activity"></a>InitializeCorrelation 活动

<xref:System.ServiceModel.Activities.InitializeCorrelation> 活动用于在不发送或接收消息的情况下初始化相关。 通常，相关是在发送或接收消息时初始化的。 如果必须在发送或接收消息前建立相关，请使用 <xref:System.ServiceModel.Activities.InitializeCorrelation> 来初始化该相关。

### <a name="using-the-initializecorrelation-activity-designer"></a>使用 InitializeCorrelation 活动设计器

访问**InitializeCorrelation**中的活动设计器**消息传送**类别**工具箱**。

**InitializeCorrelation**活动设计器可以从拖动**工具箱**和放置到工作流设计器图面。 放置在活动设计器创建<xref:System.ServiceModel.Activities.InitializeCorrelation>默认值的活动<xref:System.Activities.Activity.DisplayName%2A>InitializeCorrelation。 <xref:System.Activities.Activity.DisplayName%2A>可以在的标头中编辑**InitializeCorrelation**活动设计器中或在**DisplayName**框**属性**窗口。

<xref:System.ServiceModel.Activities.CorrelationHandle>可以是在指定**相关**字段中**属性**上的窗口**InitializeCorrelation**活动设计器图面。

若要显示**初始化相关**对话框中，您可以在其中指定相关句柄和键 / 值对用于初始化它，选择省略号按钮旁边**CorrelationData**字段中**属性**窗口。 或者，在选择"查看..."提示文本**InitializeCorrelation**活动设计器图面。 有关使用此对话框的详细信息，请参阅[类型集合编辑器对话框](../workflow-designer/type-collection-editor-dialog-box.md)一文。

### <a name="the-initializecorrelation-properties"></a>InitializeCorrelation 属性

下表显示<xref:System.ServiceModel.Activities.InitializeCorrelation>属性并说明它们如何使用在设计器中。 这些属性可以在中编辑**属性**窗口或工作流设计器图面上。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.ServiceModel.Activities.InitializeCorrelation> 活动的友好名称。 默认值为 InitializeCorrelation。<br /><br /> 虽然对友好使用非默认值<xref:System.Activities.Activity.DisplayName%2A>并非是严格要求，建议。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.Correlation%2A>|False|用于关联相关中的工作流活动的 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>|False|将消息与工作流实例相关联的相关数据的字典。<br /><br /> 使用**初始化相关**对话框可以配置<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>。 有关使用此对话框中，请参阅[类型集合编辑器对话框](../workflow-designer/type-collection-editor-dialog-box.md)一文。|

## <a name="see-also"></a>请参阅

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [Receive](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [Send](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)