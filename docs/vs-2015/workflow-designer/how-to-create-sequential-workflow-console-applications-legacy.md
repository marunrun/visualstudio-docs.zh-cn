---
title: 如何：创建顺序工作流控制台应用程序 (旧) |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c9e3f97021e742db7b22a400dee0682669b07e4c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72662732"
---
# <a name="how-to-create-sequential-workflow-console-applications-legacy"></a>如何：创建顺序工作流控制台应用程序（旧版）
按照这些步骤可使用 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 提供的旧 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 来创建顺序工作流控制台应用程序项目。 在需要面向 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 时，请使用旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。

### <a name="to-create-a-sequential-workflow-console-application"></a>创建顺序工作流控制台应用程序

1. 启动 Visual Studio。

2. 在 **“文件”** 菜单上，指向 **“新建”**，然后选择 **“项目”**。

     **“新建项目”** 对话框随即打开。

3. 在 "**新建项目**" 窗口顶部的下拉列表中选择 " **.NET Framework 3.0** " 选项或 " **.NET Framework 3.5** " 选项，以访问旧设计器。

    > [!NOTE]
    > 中的默认选项 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 是 **.NET Framework 4**。 此选项用于创建面向 [!INCLUDE[wf](../includes/wf-md.md)] 的 [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] 应用程序，并且不使用旧设计器。

4. 在 " **项目类型** " 窗格中，选择 "Visual c # 项目" 或 "Visual Basic 项目" (下的 **其他语言**) "，然后选择" **工作流**"。

5. 在 " **模板** " 窗格中选择 " **顺序工作流控制台应用程序**"。

6. 在 " **名称** " 框中，输入项目的描述性名称以便于识别。

7. 在 " **位置** " 框中，输入要保存项目的目录，或者单击 " **浏览** " 导航到该目录。

     Windows 窗体设计器将会打开并显示所创建项目的 Form1。

8. 单击" **确定**"。

     工作流设计器将会打开并显示所创建的顺序工作流的工作流设计图面。

9. 将活动从 **工具箱** 拖到 **放置活动** 指定区域中的设计图面。

## <a name="see-also"></a>另请参阅
 [创建旧版工作流项目](../workflow-designer/creating-legacy-workflow-projects.md)[开发工作流](https://msdn.microsoft.com/557bcb1f-a7ab-49f6-8df7-2706b7001301)