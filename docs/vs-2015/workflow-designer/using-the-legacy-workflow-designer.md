---
title: 使用旧工作流设计器 |Microsoft Docs
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
ms.openlocfilehash: c09c4588bb1fcd0aa7487a6896d2fc286253e198
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72606776"
---
# <a name="using-the-legacy-workflow-designer"></a>使用旧版工作流设计器
[!INCLUDE[wfd2](../includes/wfd2-md.md)] 提供的旧 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 可用于面向 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 或 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。

 可以通过在 "**新建项目**" 窗口顶部的下拉列表中选择 **.NET Framework 3.0**选项或 **.NET Framework 3.5**选项来访问它。 @No__t_0 中的默认选项是 **.NET Framework 4** ，用于创建面向 [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] 的 [!INCLUDE[wf](../includes/wf-md.md)] 应用程序。

 [!INCLUDE[wfd2](../includes/wfd2-md.md)]提供了一种以图形方式创建 [!INCLUDE[wf](../includes/wf-md.md)] 应用程序的方法（使用熟悉的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 用户界面）。 [!INCLUDE[wf](../includes/wf-md.md)] 应用程序由名为活动的工作流过程步骤组成。 若要创建工作流，请通过将活动设计器从 **"工具箱**" 拖动到设计图面上，在设计图面上撰写活动。

 下表列出了 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] for Windows Workflow Foundation 的主要功能。

|功能|描述|
|-------------|-----------------|
|活动拖放|将活动从 "**工具箱**" 拖动到设计图面上以创建工作流。|
|属性浏览器|@No__t_1 中的 "标准**属性**" 窗口用于配置活动的属性。|
|缩放|"望远镜**缩放级别**" 图标位于设计图面右侧的垂直滚动条下方。 单击望远镜并选择缩放百分比，使工作流图形放大或缩小。你还可以使用**平移**图标放大镜光标选项来放大和缩小。|
|平移|**平移**图标（包含四个方向四个十字箭头的圆圈）位于设计图面右侧垂直滚动条的下方，紧靠在望远镜缩放图标的下方。 如果单击平铺图标，一个弹出菜单将提供以下光标选项：<br /><br /> -**放大**放大镜光标允许您通过单击设计图面来放大。<br />-**缩小**放大镜光标使你可以通过单击设计图面来缩小。<br />-使用**导航工具**手动光标，可以在设计图面中 "抓取" 并移动工作流视图。<br />-**默认**的箭头光标允许您从其他光标切换回默认的箭头光标。|
|自动滚动|如果工作流很大，您可能需要将活动放在超出设计图面区域可见显示部分的位置。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 允许您将活动拖到设计图面边缘最接近您想要放置活动的位置的地方。 设计图面视图将在该方向上自动滚动。|
|智能标记|未完全配置或未有效配置的活动都标有感叹号图标。 可以单击该图标，查看活动上存在的配置需要的下拉列表。 然后，可以使用 "**属性**" 窗口来相应地配置活动。 当所有属性对于活动均有效时，感叹号图标将消失。|

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
 [开发工作流](http://go.microsoft.com/fwlink?LinkID=65010)