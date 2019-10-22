---
title: 如何：实现 Windows Communication Foundation 协定操作（旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: d6aeb20e-fac8-4a9d-bd26-ae78bef96b41
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1f6f54e781dfae15b4b1c1159d73ac3495b35c21
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72603869"
---
# <a name="how-to-implement-a-windows-communication-foundation-contract-operation-legacy"></a>如何：实现 Windows Communication Foundation 协定操作（旧版）
本主题介绍如何使用面向 [!INCLUDE[indigo1](../includes/indigo1-md.md)] 或 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 的旧 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 来实现 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 协定操作。

 将**ReceiveActivity**活动从 "工具箱" 拖到工作流设计图面后，您将创建一个新的 [!INCLUDE[indigo2](../includes/indigo2-md.md)] 合同，或者导入现有协定并实现这些操作。 您可以通过 "[选择操作" 对话框（旧版）](../workflow-designer/choose-operation-dialog-box-legacy.md)选择和/或创建协定及其操作。

### <a name="to-implement-a-wcf-contract-operation"></a>实现 WCF 协定操作

1. 在设计器中双击 " **ReceiveActivity** " 活动，或在 "**属性**" 窗格中单击 " **ServiceOperationInfo** " 属性旁边的省略号。

2. 执行以下操作之一：

   - 单击对话框右上角的 "**添加约定**"。 这将为您创建新的 [!INCLUDE[indigo2](../includes/indigo2-md.md)] 协定和操作。

      或

   - 单击对话框右上角的 "**导入**"。 "[浏览并选择 .Net 类型" 对话框（旧版）](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box-legacy.md)将打开。 搜索包含所需协定的程序集或项目。 选择合同，并单击 **"确定"** 。

     在创建或导入协定后，您可以为创建或导入的协定添加新操作。 若要添加新操作，请选择该协定，并单击对话框右上角的 "**添加操作**"。 完成添加操作后，请继续步骤 3。

3. 选择要与 " **ReceiveActivity** " 活动关联的操作。 您可以更改操作的名称、参数、属性和权限设置，从而对该操作的定义进行操作。

    若要更改名称，请在 "**操作名称**" 文本框中输入新名称。

    单击 "**参数**" 选项卡可访问该操作的参数。 您可以更改参数的名称、类型或方向，也可以在操作中添加或删除参数。

    单击 "**属性**" 选项卡以访问操作保护级别和支持的操作的消息交换功能。

    单击 "**权限**" 选项卡以指定允许哪些组执行该操作。

4. 单击 **"确定"** ，" **ReceiveActivity** " 活动将显示它正在实现的操作的操作名称。

5. 放置要用于在**ReceiveActivity**活动中实现该操作的工作流活动。

## <a name="see-also"></a>请参阅
 ["选择操作" 对话框（旧版）](../workflow-designer/choose-operation-dialog-box-legacy.md) [如何：调用 WCF 协定操作（旧版）](../workflow-designer/how-to-invoke-a-windows-communication-foundation-contract-operation-legacy.md) [旧版工作流活动](../workflow-designer/legacy-workflow-activities.md)