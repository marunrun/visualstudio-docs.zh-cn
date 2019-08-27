---
title: 如何：创建顺序工作流控制台应用程序 （旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- workflows, console applications
- sequential workflows, console applications
- console applications, sequential workflow
ms.assetid: 9f7be7fa-551f-42c6-a9bb-f5ae8ab83625
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 932b770f38f75d26028eceb6c0addc2ababeef6d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696350"
---
# <a name="how-to-create-sequential-workflow-console-applications-legacy"></a>如何：创建顺序工作流控制台应用程序（旧版）
按照这些步骤可使用 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 提供的旧 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 来创建顺序工作流控制台应用程序项目。 在需要面向 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 时，请使用旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。  
  
### <a name="to-create-a-sequential-workflow-console-application"></a>创建顺序工作流控制台应用程序  
  
1. 启动 Visual Studio。  
  
2. 在“文件”菜单上，指向“新建”，然后选择“项目”。  
  
     **“新建项目”** 对话框随即打开。  
  
3. 选择任一 **.NET Framework 3.0**选项或 **.NET Framework 3.5**中的下拉列表顶部的选项**新项目**窗口来访问旧设计器。  
  
    > [!NOTE]
    > 中的默认选项[!INCLUDE[vs2010](../includes/vs2010-md.md)]是 **.NET Framework 4**。 此选项用于创建面向 [!INCLUDE[wf](../includes/wf-md.md)] 的 [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] 应用程序，并且不使用旧设计器。  
  
4. 在中**项目类型**窗格中，选择 Visual C# 项目或 Visual Basic 项目 (在**其他语言**)，然后选择**工作流**。  
  
5. 在中**模板**窗格中，选择**顺序工作流控制台应用程序**。  
  
6. 在中**名称**框中，输入您的项目以使其容易识别的描述性名称。  
  
7. 在中**位置**框中，输入想要保存你的项目，或者单击的目录**浏览**以导航到它。  
  
     Windows 窗体设计器将会打开并显示所创建项目的 Form1。  
  
8. 单击 **“确定”**。  
  
     工作流设计器将会打开并显示所创建的顺序工作流的工作流设计图面。  
  
9. 将从活动拖放**工具箱**到中的设计图面**放置活动**指定区域。  
  
## <a name="see-also"></a>请参阅  
 [创建旧版工作流项目](../workflow-designer/creating-legacy-workflow-projects.md)   
 [开发工作流](https://msdn.microsoft.com/557bcb1f-a7ab-49f6-8df7-2706b7001301)