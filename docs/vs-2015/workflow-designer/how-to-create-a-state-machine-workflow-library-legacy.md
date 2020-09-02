---
title: 如何： (旧) 创建状态机工作流库 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- projects, state machine workflow library
- state machine workflow libraries
- workflows, state machine workflow library
ms.assetid: 5bd68c6e-6a98-47d9-826d-9bb7a4fd72f8
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d3cff5d6aaa28915524b7699affdf41d3bebef4a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72663381"
---
# <a name="how-to-create-a-state-machine-workflow-library-legacy"></a>如何：创建一个状态机工作流库（旧版）
按照这些步骤可使用 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 提供的旧 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 来创建状态机工作流库项目。 在需要面向 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 时，请使用旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。

### <a name="to-create-a-state-machine-workflow-library-project"></a>创建一个状态机工作流库项目

1. 启动 Visual Studio。

2. 在 **“文件”** 菜单上，指向 **“新建”**，然后选择 **“项目”**。

     **“新建项目”** 对话框随即打开。

3. 在 "**新建项目**" 窗口顶部的下拉列表中选择 " **.NET Framework 3.0** " 选项或 " **.NET Framework 3.5** " 选项，以访问旧设计器。

    > [!NOTE]
    > 中的默认选项 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 是 **.NET Framework 4**。 此选项用于创建面向 [!INCLUDE[wf](../includes/wf-md.md)] 的 [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] 应用程序，并且不使用旧设计器。

4. 在 " **项目类型** " 窗格中，选择 "Visual c #" 或 " **其他) 语言** Visual Basic ("，然后选择 " **工作流**"。

5. 在 " **模板** " 窗格中，选择 " **状态机工作流库**"。

6. 在 " **名称** " 框中，输入项目的描述性名称以便于识别。

7. 在 " **位置** " 框中，输入要保存项目的目录，或者单击 " **浏览** " 导航到该目录。

     如果要为项目创建解决方案目录，请选中 " **创建解决方案的目录** " 复选框，并在 " **解决方案名称** " 框中输入名称。

8. 单击“确定”。

## <a name="see-also"></a>另请参阅
 [创建旧版工作流项目](../workflow-designer/creating-legacy-workflow-projects.md)[状态机工作流](https://msdn.microsoft.com/library/344caacd-bf3b-4716-bd5a-eca74fc5a61d)