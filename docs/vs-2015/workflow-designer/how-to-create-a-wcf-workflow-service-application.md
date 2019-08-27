---
title: 如何：创建 WCF 工作流服务应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 12d675ac-27d8-4d86-ba16-6f7688f8c841
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d0c258ea081e95179c507f76413ae2a5fc7d71a5
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65705854"
---
# <a name="how-to-create-a-wcf-workflow-service-application"></a>如何：创建 WCF 工作流服务应用程序
[!INCLUDE[indigo1](../includes/indigo1-md.md)] 工作流服务应用程序是在它们自身与客户端之间跨进程边界传递消息的分布式通信服务。 服务端服务协定的实现是通过 [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] 中的工作流活动，以类似于 .NET Framework 3.5 中的旧工作流服务的方式基于声明完成的。  
  
### <a name="to-create-a-wcf-workflow-service-application"></a>创建 WCF 工作流服务应用程序  
  
1. 启动 [!INCLUDE[vs2010](../includes/vs2010-md.md)]。  
  
2. 上**文件**菜单，依次指向**新建**，然后选择**项目...**.  
  
     **“新建项目”** 对话框随即打开。  
  
3. 在中**已安装的模板**窗格中，选择**WCF**或**工作流**眖**Visual C#** 或**Visual Basic**具体取决于所选的语言的分组。  
  
4. 在中间窗格中，选择**WCF 工作流服务应用程序**。  
  
5. 在中**名称**框中，输入您的项目以使其容易识别的描述性名称。  
  
6. 在中**位置**框中，输入想要保存你的项目，或者单击的目录**浏览**以导航到它。  
  
7. 在中**解决方案**框中，选择此选项创建新的解决方案，然后单击**确定**。  
  
    > [!NOTE]
    > 如果你想要添加到现有解决方案工作流控制台应用程序，打开该解决方案[!INCLUDE[vs2010](../includes/vs2010-md.md)]，右键单击中的解决方案**解决方案资源管理器**，然后选择**添加**，然后**新建项目...** 若要打开**新的项目**对话框。 按照此过程中的上述步骤继续操作。  
  
8. 该项目模板将创建一个 XAML 格式的服务定义。 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 打开设计视图，其中显示一个 <xref:System.Activities.Statements.Sequence> 活动，该活动包含一组 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动。  
  
## <a name="see-also"></a>请参阅  
 [如何：创建活动](https://msdn.microsoft.com/library/c09b1e99-21b5-4d96-9c04-ec31db3f4436)   
 [创建工作流项目](../workflow-designer/creating-a-workflow-project.md)