---
title: 顺序工作流视图 （旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- sequential workflow views
- sequential workflows, views
ms.assetid: 135f24b9-1b37-442b-9ef8-f0f2108a3212
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 97d13a86e8bade0855c60326996a192a0d0331b3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62938538"
---
# <a name="sequential-workflow-views-legacy"></a>顺序工作流视图（旧版）
[!INCLUDE[vs2010](../includes/vs2010-md.md)] 提供了一个旧 [!INCLUDE[wfd1](../includes/wfd1-md.md)]，可用于面向 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 或 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。  
  
 [!INCLUDE[wfd2](../includes/wfd2-md.md)]提供了一种以图形方式创建 [!INCLUDE[wf](../includes/wf-md.md)] 应用程序的方法（使用熟悉的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 用户界面）。 [!INCLUDE[wf](../includes/wf-md.md)] 应用程序由名为活动的工作流过程步骤组成。 若要创建工作流，构成活动设计图面上的，通过拖动其各自的活动设计器从**工具箱**拖到设计图面。  
  
 当创建顺序工作流，即[SequentialWorkflowActivity](http://go.microsoft.com/fwlink?LinkID=65040)，提供了三个工作流视图。 这些视图是从可访问**工作流**菜单和设计图面上的上下文菜单。  
  
 下表列出了每个视图的名称和说明。  
  
|菜单/选项卡选项|描述|  
|----------------------|-----------------|  
|**查看顺序**|右键单击设计图面，然后选择**查看顺序**上下文菜单中的选项以显示**顺序工作流**视图，其中显示了基于活动的图形顺序工作流的表示形式。 或选择**查看顺序**从**工作流**菜单。|  
|**查看取消处理程序**|右键单击设计图面，然后选择**查看取消处理程序**上下文菜单中的选项以显示**顺序工作流**视图，视图的显示[CancellationHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65050)与工作流关联的活动。 或选择**查看取消处理程序**从**工作流**菜单。|  
|**查看错误处理程序**|右键单击设计图面，然后选择**查看错误处理程序**上下文菜单中的选项以显示**错误**视图，视图的显示[FaultHandlersActivity](http://go.microsoft.com/fwlink?LinkID=65055)与工作流关联的活动。 或选择**查看错误处理程序**从**工作流**菜单。|  
  
 有关类似视图的详细信息，请参阅[活动视图 （旧版）](../workflow-designer/activity-views-legacy.md)。  
  
## <a name="see-also"></a>请参阅  
 [活动视图 （旧版）](../workflow-designer/activity-views-legacy.md)   
 [创建旧版工作流项目](../workflow-designer/creating-legacy-workflow-projects.md)   
 [工作流创作模式](http://go.microsoft.com/fwlink?LinkID=65014)