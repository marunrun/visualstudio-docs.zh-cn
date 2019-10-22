---
title: 如何：调用 Windows Communication Foundation 协定操作（旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: a9058345-708f-4fcf-8739-2a43e5285b7a
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6f42600a739561a27a6dd8f6caa237027bac4554
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72603707"
---
# <a name="how-to-invoke-a-windows-communication-foundation-contract-operation-legacy"></a>如何：调用 Windows Communication Foundation 协定操作（旧版）
本主题介绍如何使用面向 [!INCLUDE[indigo1](../includes/indigo1-md.md)] 或 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 的旧 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 来调用 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 协定操作。

 在将 " **SendActivity** " 活动从 "工具箱" 拖到工作流设计图面之后，必须导入现有协定，并确定将从该**SendActivity**活动中调用的操作。 可以通过 "[选择操作" 对话框（旧版）](../workflow-designer/choose-operation-dialog-box-legacy.md)选择协定及其操作。

 另外，如果您一起使用配置文件和服务，则您需要指定一个 <xref:System.Workflow.Activities.ChannelToken>。 <xref:System.Workflow.Activities.ChannelToken> 标识终结点配置，发送活动将使用此终结点配置来连接到工作流服务。

### <a name="to-invoke-a-wcf-contract-operation-from-a-sendactivity-activity"></a>从 SendActivity 活动调用 WCF 协定操作

1. 在设计器中双击 " **SendActivity** " 活动，或在 "**属性**" 窗格中单击 " **ServiceOperationInfo** " 属性旁边的省略号。

2. 当 "**选择操作**" 对话框打开时，单击对话框右上角的 "**导入**"。

     "[浏览并选择 .Net 类型" 对话框（旧版）](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box-legacy.md)将打开。

3. 搜索包含所需协定的程序集或项目。

4. 选择合同，并单击 **"确定"** 。

5. 在 "**可用操作**" 下，选择要调用的操作，然后单击 **"确定"** 。

### <a name="to-specify-a-channel-token"></a>指定通道令牌

1. 在设计器中选择 <xref:System.Workflow.Activities.SendActivity> 活动。

2. 在 "**属性**" 窗格中，指定 <xref:System.Workflow.Activities.ChannelToken> 的名称。 此名称唯一标识通道令牌。

3. 展开通道令牌节点，并为要在 <xref:System.Workflow.Activities.ChannelToken.EndpointName%2A> 字段中使用的客户端终结点指定名称。 配置文件中名称相同的终结点配置将用于配置通道。

4. 如果配置文件中不存在终结点配置，请创建终结点配置。 有关配置客户端的详细信息，请参阅[WCF 客户端概述](https://msdn.microsoft.com/library/f60d9bc5-8ade-4471-8ecf-5a07a936c82d)。

## <a name="see-also"></a>请参阅
 ["选择操作" 对话框（旧版）](../workflow-designer/choose-operation-dialog-box-legacy.md) [如何：实现 WCF 协定操作（旧版）](../workflow-designer/how-to-implement-a-windows-communication-foundation-contract-operation-legacy.md) [旧版工作流活动](../workflow-designer/legacy-workflow-activities.md)