---
title: "\"选择操作\" 对话框（旧版） |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Workflow.Activities.Design.OperationPickerDialog.UI
ms.assetid: bc3ec902-7797-494e-af48-e70c97eb6779
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f2736db7e18733a9477238cafad21088eb135e89
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659161"
---
# <a name="choose-operation-dialog-box-legacy"></a>“选择操作”对话框（旧版）
本主题介绍如何使用旧 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 中的 "**选择操作**" 对话框。 在需要面向 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 时，请使用旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。

 "**选择操作**" 对话框用于选择要与 <xref:System.Workflow.Activities.ReceiveActivity> 活动或 <xref:System.Workflow.Activities.SendActivity> 活动关联的操作。 有关将此对话框与这些活动一起使用的详细信息，请参阅 [How：实现 WCF 协定操作（旧版） ](../workflow-designer/how-to-implement-a-windows-communication-foundation-contract-operation-legacy.md)，并将 [How 到：调用 WCF 协定操作（旧版） ](../workflow-designer/how-to-invoke-a-windows-communication-foundation-contract-operation-legacy.md)。

 下表介绍 "**选择操作**" 对话框的用户界面（UI）元素。

|UI 元素|说明|
|----------------|-----------------|
|**添加协定**|为您创建一个新协定。 您可以在此协定上定义新操作。 （仅与 <xref:System.Workflow.Activities.ReceiveActivity> 一起使用。）|
|**添加操作**|向在 "**选择操作**" 对话框中创建的新约定添加新操作。 **注意：** 只能向通过 "**选择操作**" 对话框创建的约定添加新操作。 <br /><br /> （仅与 <xref:System.Workflow.Activities.ReceiveActivity> 一起使用。）|
|**导入 .。。**|导入以前定义的协定，并允许您从该协定中选择一种操作。|
|**操作名称**|当前选定操作的名称。 仅当通过 "**选择操作**" 对话框创建了操作后，此文本框才可用。|
|**参数**|此选项卡包含当前选定操作的参数定义。 **注意：** 仅当通过 "**选择操作**" 对话框创建了操作后，才能更改参数定义。|
|**属性**|此选项卡包含在客户端和服务之间所发送消息的 <xref:System.Net.Security.ProtectionLevel> 设置。 **注意：** 仅当通过 "**选择操作**" 对话框创建操作时，才启用此选项卡。|
|**权限**|此选项卡包含允许调用此操作的用户的 <xref:System.Workflow.Activities.OperationInfoBase.PrincipalPermissionName%2A> 和 <xref:System.Workflow.Activities.OperationInfoBase.PrincipalPermissionRole%2A> 属性。 例如，如果只允许 Administrators 组中的用户调用该操作，则会在 "**角色**" 文本框中编写 "Administrators"。<br /><br /> 通过 " **ChooseOperation** " 对话框和通过 "**导入**" 按钮导入的操作，启用此选项卡。|

> [!NOTE]
> "**选择操作**" 对话框仅显示工作流中的其他 <xref:System.Workflow.Activities.SendActivity> 活动所使用的协定或操作。 同样，<xref:System.Workflow.Activities.ReceiveActivity> 活动的 "**选择操作**" 对话框仅显示工作流中的其他**ReceiveActivity**活动所使用的协定或操作。

## <a name="see-also"></a>请参阅
 [如何：实现 WCF 协定操作（旧版） ](../workflow-designer/how-to-implement-a-windows-communication-foundation-contract-operation-legacy.md) [How：调用 WCF 协定操作（旧版） ](../workflow-designer/how-to-invoke-a-windows-communication-foundation-contract-operation-legacy.md)[旧版设计器以 Windows Workflow Foundation 用户界面帮助](../workflow-designer/legacy-designer-for-windows-workflow-foundation-ui-help.md)