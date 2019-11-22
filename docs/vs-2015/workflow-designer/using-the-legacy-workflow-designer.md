---
title: Using the Legacy Workflow Designer | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- Visual Studio 2005 Extensions for Windows Workflow Foundation, about
ms.assetid: 7af53077-afd7-465f-9c1d-b387e9d4f216
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2fa11cd0b29f3b8ee6008b8c0b3369b16812f0e5
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302789"
---
# <a name="using-the-legacy-workflow-designer"></a>使用旧版工作流设计器
[!INCLUDE[wfd2](../includes/wfd2-md.md)] 提供的旧 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 可用于面向 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 或 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。

 It is accessed by selecting either the **.NET Framework 3.0** option or the **.NET Framework 3.5** option in the drop down list at the top of the **New Project** window. The default option in [!INCLUDE[vs2010](../includes/vs2010-md.md)] is **.NET Framework 4** which is used to create [!INCLUDE[wf](../includes/wf-md.md)] applications that target the [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)].

 [!INCLUDE[wfd2](../includes/wfd2-md.md)]提供了一种以图形方式创建 [!INCLUDE[wf](../includes/wf-md.md)] 应用程序的方法（使用熟悉的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 用户界面）。 [!INCLUDE[wf](../includes/wf-md.md)] 应用程序由名为活动的工作流过程步骤组成。 To create a workflow, compose activities on the design surface by dragging their respective activity designers from **Toolbox** onto the design surface.

 下表列出了 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] for Windows Workflow Foundation 的主要功能。

|功能|描述|
|-------------|-----------------|
|活动拖放|Drag activities from the **Toolbox** onto the design surface to create a workflow.|
|属性浏览器|The standard **Properties** window in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] is used to configure the properties of an activity.|
|缩放|The binoculars **Zoom Level** icon is located below the vertical scroll bar on the right side of the design surface. Click the binoculars and select a zoom percentage to cause the workflow graphic to zoom in or out. You can also use the **Pan** icon magnifying glass cursor options to zoom in and out.|
|平移|The **Pan** icon, a circle that contains four crossed arrows pointing in four directions, is located below the vertical scroll bar on the right side of the design surface just below the binoculars zoom icon. 如果单击平铺图标，一个弹出菜单将提供以下光标选项：<br /><br /> -   The **Zoom In** magnifying glass cursor lets you zoom in by clicking the design surface.<br />-   The **Zoom Out** magnifying glass cursor lets you zoom out by clicking the design surface.<br />-   The **Navigation Tool** hand cursor lets you "grab" and shift the view of a workflow in the design surface.<br />-   The **Default** arrow cursor lets you switch from the other cursors back to the default arrow cursor.|
|自动滚动|如果工作流很大，您可能需要将活动放在超出设计图面区域可见显示部分的位置。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 允许您将活动拖到设计图面边缘最接近您想要放置活动的位置的地方。 设计图面视图将在该方向上自动滚动。|
|智能标记|未完全配置或未有效配置的活动都标有感叹号图标。 可以单击该图标，查看活动上存在的配置需要的下拉列表。 You can then use the **Properties** window to configure the activity appropriately. 当所有属性对于活动均有效时，感叹号图标将消失。|

## <a name="in-this-section"></a>本节内容
 [Visual Studio 工作流窗口（旧版）](../workflow-designer/visual-studio-workflow-windows-legacy.md)

 [创建旧版工作流项目](../workflow-designer/creating-legacy-workflow-projects.md)

 [顺序工作流视图（旧版）](../workflow-designer/sequential-workflow-views-legacy.md)

 [旧版工作流活动](../workflow-designer/legacy-workflow-activities.md)

 [在工作流中使用主题（旧版）](../workflow-designer/using-themes-in-workflows-legacy.md)

 [使用旧版状态机工作流设计器](../workflow-designer/using-the-legacy-state-machine-workflow-designer.md)

 [使用旧版活动设计器](../workflow-designer/using-the-legacy-activity-designer.md)

 [Windows Workflow Foundation 的旧版设计器 UI 帮助](../workflow-designer/legacy-designer-for-windows-workflow-foundation-ui-help.md)

## <a name="see-also"></a>请参阅
 [Developing Workflows](https://go.microsoft.com/fwlink?LinkID=65010)