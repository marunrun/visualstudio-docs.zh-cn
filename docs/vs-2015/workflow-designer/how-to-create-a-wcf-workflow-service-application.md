---
title: 如何：创建 WCF 工作流服务应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 12d675ac-27d8-4d86-ba16-6f7688f8c841
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9bf941babd943c6856809a13de847b62745b2056
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72605017"
---
# <a name="how-to-create-a-wcf-workflow-service-application"></a>如何：创建 WCF 工作流服务应用程序
[!INCLUDE[indigo1](../includes/indigo1-md.md)] 工作流服务应用程序是在它们自身与客户端之间跨进程边界传递消息的分布式通信服务。 服务端服务协定的实现是通过 [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] 中的工作流活动，以类似于 .NET Framework 3.5 中的旧工作流服务的方式基于声明完成的。

### <a name="to-create-a-wcf-workflow-service-application"></a>创建 WCF 工作流服务应用程序

1. 启动 [!INCLUDE[vs2010](../includes/vs2010-md.md)]。

2. 在 "**文件**" 菜单上，指向 "**新建**"，然后选择 "**项目 ...** "。

     **“新建项目”** 对话框随即打开。

3. 在 "**已安装的模板**" 窗格中，根据所选的语言，从 **C#视觉对象**或**Visual Basic**分组中选择 " **WCF** " 或 "**工作流**"。

4. 在中间窗格中，选择 " **WCF 工作流服务应用程序**"。

5. 在 "**名称**" 框中，输入项目的描述性名称以便于识别。

6. 在 "**位置**" 框中，输入要保存项目的目录，或者单击 "**浏览**" 导航到该目录。

7. 在 "**解决方案**" 框中，选择 "新建解决方案"，然后单击 **"确定"** 。

    > [!NOTE]
    > 如果要向现有解决方案添加工作流控制台应用程序，请在 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 中打开该解决方案，右键单击**解决方案资源管理器**中的解决方案，然后依次选择 "**添加**"、"**新建项目 ...** " 打开 "**新建项目**" 对话框。 按照此过程中的上述步骤继续操作。

8. 该项目模板将创建一个 XAML 格式的服务定义。 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 打开设计视图，其中显示一个 <xref:System.Activities.Statements.Sequence> 活动，该活动包含一组 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动。

## <a name="see-also"></a>请参阅
 [如何：创建](https://msdn.microsoft.com/library/c09b1e99-21b5-4d96-9c04-ec31db3f4436)[创建工作流项目](../workflow-designer/creating-a-workflow-project.md)的活动