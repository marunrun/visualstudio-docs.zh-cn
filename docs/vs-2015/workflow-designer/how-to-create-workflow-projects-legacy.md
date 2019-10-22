---
title: 如何：创建工作流项目（旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- workflow projects, creating
- projects, workflow
ms.assetid: 32299555-662c-469d-a90d-89f4700dc78c
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3cf68c1a28f662bfa4e271d3c402ef1c8946b6f1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668679"
---
# <a name="how-to-create-workflow-projects-legacy"></a>如何：创建工作流项目（旧版）
按照这些步骤可创建面向 [!INCLUDE[wf](../includes/wf-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 的 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 项目。 此过程使用由 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 提供的旧 [!INCLUDE[vs2010](../includes/vs2010-md.md)]。

### <a name="to-create-a-workflow-project"></a>创建一个工作流项目

1. 启动 [!INCLUDE[vs_current_long](../includes/vs-current-long-md.md)]。

2. 在“文件”菜单上，指向“新建”，然后选择“项目”。

     **“新建项目”** 对话框随即打开。

3. 在 "**新建项目**" 窗口顶部的下拉列表中选择 " **.NET Framework 3.0** " 选项或 " **.NET Framework 3.5** " 选项，以访问旧设计器。

    > [!NOTE]
    > @No__t_0 中的默认选项为 **.NET Framework 4**。 此选项用于创建面向 [!INCLUDE[wf](../includes/wf-md.md)] 的 [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] 应用程序，并且不使用旧设计器。

4. 在 "**项目类型**" 窗格中， C#选择 "可视项目" 或 "Visual Basic 项目"，然后选择 "**工作流**"。

5. 在 "**模板**" 窗格中，选择一个已安装的项目模板：

    - 顺序工作流控制台应用程序

    - 顺序工作流库

    - 工作流 Activity 库

    - 状态机工作流控制台应用程序

    - 状态机工作流库

    - 空工作流项目

6. 在 "**名称**" 框中，输入项目的描述性名称以便于识别。

7. 在 "**位置**" 框中，输入要保存项目的目录，或者单击 "**浏览**" 导航到该目录。

     如果要为项目创建解决方案目录，请选中 "**创建解决方案的目录**" 复选框，并在 "**解决方案名称**" 框中输入名称。

8. 单击“确定”。

## <a name="see-also"></a>请参阅
 [创建旧版工作流项目](../workflow-designer/creating-legacy-workflow-projects.md)