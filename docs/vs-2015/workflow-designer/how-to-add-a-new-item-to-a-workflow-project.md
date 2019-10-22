---
title: 如何：向工作流项目添加新项 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 5c6180ca-af10-4513-b0cb-7d478fd84eab
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 004f079576b792fb76d596ee8ebac3f6f96f316e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656631"
---
# <a name="how-to-add-a-new-item-to-a-workflow-project"></a>如何：向工作流项目添加新项
创建工作流项目之后，可以将工作流活动、设计器和其他熟悉的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项添加到项目中。

 下表列出了可添加到工作流项目中的 [!INCLUDE[wf](../includes/wf-md.md)] 项。

|“属性”|描述|
|----------|-----------------|
|活动|由其他活动组成的活动。 选择此项可将相同的 XAML 文件添加到项目中，就像为新项目选择 "**活动库**" 模板时所获得的那样。 [!INCLUDE[crabout](../includes/crabout-md.md)] 此过程，请参阅[如何：创建活动库](../workflow-designer/how-to-create-an-activity-library.md)。|
|活动设计器|用于自定义活动的设计时体验的设计器。 选择此项可将相同文件添加到项目中，就像在为新项目选择 "**活动设计器库**" 模板时所获得的一样。 [!INCLUDE[crabout](../includes/crabout-md.md)] 此过程的说明，请参阅[如何：创建活动设计器库](../workflow-designer/how-to-create-an-activity-designer-library.md)。|
|Code 活动|一个采用代码编写执行逻辑的活动。 已为你生成一个源代码文件，该文件带有 <xref:System.Activities.CodeActivity.Execute%2A> 方法的重写。|
|WCF 工作流服务|使用工作流活动生成的 [!INCLUDE[indigo2](../includes/indigo2-md.md)] 服务。 选择此项可将相同文件添加到项目中，就像在为新项目选择**WCF 工作流服务应用程序**模板时所获得的一样。 [!INCLUDE[crabout](../includes/crabout-md.md)] 此过程的说明，请参阅[如何：创建 WCF 工作流服务应用程序](../workflow-designer/how-to-create-a-wcf-workflow-service-application.md)。|

### <a name="to-add-a-new-item-to-a-workflow-project"></a>向工作流项目添加新项

1. 在 "**项目**" 菜单上，单击 "**添加新项 ...** "。

     "**添加新项**" 对话框随即打开。

2. 在 "**已安装的模板**" 窗格中选择 "**工作流**组"。

3. 选择四项中的一项。 上表列出了可用的选项。

4. 在对话框底部的 "**名称**" 框中为该项键入适当的名称。

5. 单击 "**添加**" 将该项添加到当前工作流项目中。

## <a name="see-also"></a>请参阅
 [创建工作流项目](../workflow-designer/creating-a-workflow-project.md)