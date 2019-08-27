---
title: 如何：向工作流项目添加新项 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 5c6180ca-af10-4513-b0cb-7d478fd84eab
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ecc310896f7b938025d42e06ac5ef0ec8bac3d35
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62932998"
---
# <a name="how-to-add-a-new-item-to-a-workflow-project"></a>如何：向工作流项目添加新项
创建工作流项目之后，可以将工作流活动、设计器和其他熟悉的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项添加到项目中。  
  
 下表列出了可添加到工作流项目中的 [!INCLUDE[wf](../includes/wf-md.md)] 项。  
  
|名称|描述|  
|----------|-----------------|  
|活动|由其他活动组成的活动。 选择此项将同一个 XAML 文件添加到项目，选择时要获得**活动库**新项目模板。 [!INCLUDE[crabout](../includes/crabout-md.md)] 在此过程中，请参阅[如何：创建活动库](../workflow-designer/how-to-create-an-activity-library.md)。|  
|活动设计器|用于自定义活动的设计时体验的设计器。 选择此项将相同文件添加到项目，选择时要获得**活动设计器库**新项目模板。 [!INCLUDE[crabout](../includes/crabout-md.md)] 在此过程中，请参阅[如何：创建活动设计器库](../workflow-designer/how-to-create-an-activity-designer-library.md)。|  
|Code 活动|一个采用代码编写执行逻辑的活动。 已为你生成一个源代码文件，该文件带有 <xref:System.Activities.CodeActivity.Execute%2A> 方法的重写。|  
|WCF 工作流服务|使用工作流活动生成的 [!INCLUDE[indigo2](../includes/indigo2-md.md)] 服务。 选择此项将相同文件添加到项目，选择时要获得**WCF 工作流服务应用程序**新项目模板。 [!INCLUDE[crabout](../includes/crabout-md.md)] 在此过程中，请参阅[如何：创建 WCF 工作流服务应用程序](../workflow-designer/how-to-create-a-wcf-workflow-service-application.md)。|  
  
### <a name="to-add-a-new-item-to-a-workflow-project"></a>向工作流项目添加新项  
  
1. 上**项目**菜单上，单击**添加新项...**.  
  
     **添加新项**对话框随即打开。  
  
2. 在中**已安装的模板**窗格中，选择**工作流**组。  
  
3. 选择四项中的一项。 上表列出了可用的选项。  
  
4. 键入相应的名称中的项**名称**对话框底部的框。  
  
5. 单击**添加**将项添加到当前工作流项目。  
  
## <a name="see-also"></a>请参阅  
 [创建工作流项目](../workflow-designer/creating-a-workflow-project.md)