---
title: 如何：向工作流项目添加新项（旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- sequential workflows, adding to workflow projects
- workflows, adding new items
- state machine workflows, adding to workflow projects
- activities, adding to workflow projects
ms.assetid: 130cd83d-942d-437b-bbb5-8088ec0a6d79
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 46f6e9daafc2688b9bea75cba9eddd8c8a53c9bb
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656673"
---
# <a name="how-to-add-a-new-item-to-a-workflow-project-legacy"></a>如何：向工作流项目添加新项（旧版）
在使用 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 提供的、面向 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 的旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 创建工作流项目之后，可向该项目添加 [!INCLUDE[wf](../includes/wf-md.md)] 项和其他熟悉的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项。

 下表列出了可添加到工作流项目中的 [!INCLUDE[wf2](../includes/wf2-md.md)] 项。

|项|描述|
|----------|-----------------|
|活动|活动定义在设计器代码文件中而用户代码在另一个代码文件中的活动。|
|Activity (具有单独的代码)|位于不同代码文件中的活动定义（以工作流标记形式表示）和用户代码。|
|顺序工作流 (代码)|工作流定义在设计器代码文件中而用户代码在另一个代码文件中的顺序工作流。|
|顺序工作流 (具有单独的代码)|工作流定义（以工作流标记形式表示）与用户代码位于不同代码文件中的顺序工作流。|
|状态机工作流 (代码)|工作流定义在设计器代码文件中而用户代码在另一个代码文件中的状态机工作流。|
|状态机工作流 (具有单独的代码)|工作流定义（以工作流标记形式表示）与用户代码位于不同代码文件中的状态机工作流。|

### <a name="to-add-a-new-item-to-a-workflow-project"></a>向工作流项目添加新项

1. 在 "**项目**" 菜单上，单击 "**添加新项**"。

     "**添加新项**" 对话框随即打开。

2. 选择一个项。

     前面的表列出了可用的 Windows Workflow Foundation 选择。

3. 单击 "**添加**" 将该项添加到工作流项目中。

## <a name="see-also"></a>请参阅
 [创建旧版工作流项目](../workflow-designer/creating-legacy-workflow-projects.md)