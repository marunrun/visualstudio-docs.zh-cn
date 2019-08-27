---
title: 如何：调用 Windows Communication Foundation 协定操作 （旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: a9058345-708f-4fcf-8739-2a43e5285b7a
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 1398d7fb62943c04ca026175a3f46b282bf6da69
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696323"
---
# <a name="how-to-invoke-a-windows-communication-foundation-contract-operation-legacy"></a>如何：调用 Windows Communication Foundation 协定操作（旧版）
本主题介绍如何使用面向 [!INCLUDE[indigo1](../includes/indigo1-md.md)] 或 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 的旧 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 来调用 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 协定操作。  
  
 之后**SendActivity**活动从工具箱拖到工作流设计图面，必须导入现有协定，并确定将从该调用哪些操作**SendActivity**活动。 选择协定及其操作通过[选择操作对话框 （旧版）](../workflow-designer/choose-operation-dialog-box-legacy.md)。  
  
 另外，如果您一起使用配置文件和服务，则您需要指定一个 <xref:System.Workflow.Activities.ChannelToken>。 <xref:System.Workflow.Activities.ChannelToken> 标识终结点配置，发送活动将使用此终结点配置来连接到工作流服务。  
  
### <a name="to-invoke-a-wcf-contract-operation-from-a-sendactivity-activity"></a>从 SendActivity 活动调用 WCF 协定操作  
  
1. 双击**SendActivity**活动设计器中的，或单击省略号旁边**ServiceOperationInfo**中的属性**属性**窗格。  
  
2. 当**选择操作**对话框打开，请单击**导入**右上角的对话框。  
  
     [浏览并选择.NET 类型对话框 （旧版）](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box-legacy.md)随即打开。  
  
3. 搜索包含所需协定的程序集或项目。  
  
4. 选择该协定，然后单击**确定**。  
  
5. 下**可用的操作**，选择你想要调用，单击的操作**确定**。  
  
### <a name="to-specify-a-channel-token"></a>指定通道令牌  
  
1. 在设计器中选择 <xref:System.Workflow.Activities.SendActivity> 活动。  
  
2. 在中**属性**窗格中，指定的名称<xref:System.Workflow.Activities.ChannelToken>。 此名称唯一标识通道令牌。  
  
3. 展开通道令牌节点，并为要在 <xref:System.Workflow.Activities.ChannelToken.EndpointName%2A> 字段中使用的客户端终结点指定名称。 配置文件中名称相同的终结点配置将用于配置通道。  
  
4. 如果配置文件中不存在终结点配置，请创建终结点配置。 有关配置客户端的详细信息，请参阅[WCF 客户端概述](https://msdn.microsoft.com/library/f60d9bc5-8ade-4471-8ecf-5a07a936c82d)。  
  
## <a name="see-also"></a>请参阅  
 [选择操作对话框 （旧版）](../workflow-designer/choose-operation-dialog-box-legacy.md)   
 [如何：实现 WCF 协定操作 （旧版）](../workflow-designer/how-to-implement-a-windows-communication-foundation-contract-operation-legacy.md)   
 [旧版工作流活动](../workflow-designer/legacy-workflow-activities.md)