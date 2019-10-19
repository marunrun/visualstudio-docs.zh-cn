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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b6ffcfd63d60ab6f085b5cb2a793e8bf17a50d8e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656913"
---
# <a name="correlationscope-activity-designer"></a>CorrelationScope 活动设计器
" **CorrelationScope** " 活动设计器用于创建和配置 <xref:System.ServiceModel.Activities.CorrelationScope> 活动，该活动使用 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象提供子消息传递活动的隐式管理。

## <a name="the-correlationscope-activity"></a>CorrelationScope 活动
 <xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A> 属性指定用于管理子消息传递活动的 <xref:System.ServiceModel.Activities.CorrelationHandle>。 将 <xref:System.ServiceModel.Activities.Send> 中包含的 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.CorrelationScope.Body%2A> 活动配置为使用包含 <xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A> 活动的 <xref:System.ServiceModel.Activities.CorrelationScope> 属性以执行相关。

### <a name="using-the-correlationscope-activity-designer"></a>使用 CorrelationScope 活动设计器
 " **CorrelationScope** " 活动设计器可在 "**工具箱**" 的 "**消息传送**" 类别中找到，可通过单击 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 左侧的 "**工具箱**" 选项卡（或者，**从**"**视图**" 菜单或 CTRL + ALT + X。）

 可以将 " **CorrelationScope** " 活动设计器从 "**工具箱**" 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上。 这将创建具有 CorrelationScope 的默认**DisplayName**的 <xref:System.ServiceModel.Activities.CorrelationScope> 活动。 可以在 " **CorrelationScope** " 活动设计器的标头中或在 "**属性**" 窗口的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A>。

 若要指定子消息传递活动使用的 <xref:System.ServiceModel.Activities.CorrelationHandle>，请在 "**属性**" 窗口中单击 " **CorrelatesWith** " 字段旁边的省略号按钮，以显示 "**表达式编辑器**" 对话框。 还可以在活动设计器图面上设置此属性。

 在相关范围内的活动是通过在**CorrelationScope**设计器内的 "**正文**" 框中删除其设计器来指定的。

### <a name="the-correlationscope-properties"></a>CorrelationScope 属性
 下表列出 <xref:System.ServiceModel.Activities.CorrelationScope> 属性并说明如何在设计器中使用它们。 这些属性可以在 "**属性**" 窗口或 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 设计器图面上进行编辑，也可以在这两种情况下编辑。

|属性名|必需|用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.ServiceModel.Activities.InitializeCorrelation> 活动的可选友好名称。|
|<xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A>|False|指定用于管理子消息传递活动的 <xref:System.ServiceModel.Activities.CorrelationHandle>。 如果未设置此属性，则 <xref:System.ServiceModel.Activities.CorrelationScope> 会自动创建一个隐式 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|<xref:System.ServiceModel.Activities.CorrelationScope.Body%2A>|False|指定处于相关范围之内的活动。|

## <a name="see-also"></a>请参阅
 [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md) [Receive](../workflow-designer/receive-activity-designer.md) [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md) [Send](../workflow-designer/send-activity-designer.md) [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md) [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)