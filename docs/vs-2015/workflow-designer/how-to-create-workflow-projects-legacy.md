---
title: 如何：创建工作流项目 （旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- workflow projects, creating
- projects, workflow
ms.assetid: 32299555-662c-469d-a90d-89f4700dc78c
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 6d779294f991786f90faf8dd1de756749b6baffc
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444162"
---
# <a name="how-to-create-workflow-projects-legacy"></a>如何：创建工作流项目（旧版）
按照这些步骤可创建面向 [!INCLUDE[wf](../includes/wf-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 的 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 项目。 此过程使用由 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 提供的旧 [!INCLUDE[vs2010](../includes/vs2010-md.md)]。  
  
### <a name="to-create-a-workflow-project"></a>创建一个工作流项目  
  
1. 启动 [!INCLUDE[vs_current_long](../includes/vs-current-long-md.md)]。  
  
2. 在“文件”菜单上，指向“新建”，然后选择“项目”。  
  
     **“新建项目”** 对话框随即打开。  
  
3. 选择任一 **.NET Framework 3.0**选项或 **.NET Framework 3.5**中的下拉列表顶部的选项**新项目**窗口来访问旧设计器。  
  
    > [!NOTE]
    > 中的默认选项[!INCLUDE[vs2010](../includes/vs2010-md.md)]是 **.NET Framework 4**。 此选项用于创建面向 [!INCLUDE[wf](../includes/wf-md.md)] 的 [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] 应用程序，并且不使用旧设计器。  
  
4. 在中**项目类型**窗格中，选择 Visual C# 项目或 Visual Basic 项目，然后选择**工作流**。  
  
5. 在中**模板**窗格中，选择一个已安装的项目模板：  
  
    - 顺序工作流控制台应用程序  
  
    - 顺序工作流库  
  
    - 工作流 Activity 库  
  
    - 状态机工作流控制台应用程序  
  
    - 状态机工作流库  
  
    - 空工作流项目  
  
6. 在中**名称**框中，输入您的项目以使其容易识别的描述性名称。  
  
7. 在中**位置**框中，输入想要保存你的项目，或者单击的目录**浏览**以导航到的目录。  
  
     如果您希望为项目创建一个解决方案目录，选择**创建解决方案目录**复选框并输入中的名称**解决方案名称**框。  
  
8. 单击 **“确定”**。  
  
## <a name="see-also"></a>请参阅  
 [创建旧版工作流项目](../workflow-designer/creating-legacy-workflow-projects.md)