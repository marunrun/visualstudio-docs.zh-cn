---
title: 如何：调试基于 ASP.NET 的工作流（旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- ASP.NET, debugging workflows
- debugging workflows, ASP.NET workflows
- ASP.NET workflows, debugging
- debugging, ASP.NET workflows
ms.assetid: 79b21edc-9e7d-410d-af68-09c1598b9c30
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f3bed38f5229cb489f663878759517480b48302c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668658"
---
# <a name="how-to-debug-aspnet-based-workflows-legacy"></a>如何：调试基于 ASP.NET 的工作流（旧版）
本主题介绍如何在旧 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 中，调试基于 [!INCLUDE[wf](../includes/wf-md.md)] 并面向 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 或 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 的 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 应用程序。

 通过附加到承载工作流的进程，可以调试在 ASP.NET 中启动的旧工作流或以 Web 服务形式发布的旧工作流。

### <a name="to-debug-an-aspnet-based-workflow"></a>调试基于 ASP.NET 的工作流

1. 通过在 web.config 文件中设置**debug = true**来启用对 ASP.NET 应用程序的调试。

2. 将工作流库设置为启动项目，并在工作流上设置断点。

3. 在工作流项目属性 "**调试**选项" "**启动浏览器与外部 URL** " 文本框中输入默认网页的 URL。

4. 选择 "**调试**" 菜单上的 "**附加到进程**"。

5. 从 "**可用进程**" 列表中选择要附加到的进程。

     附加到承载工作流的 w3wp.exe、webdev.webserver 或 aspnet_wp 进程。

6. 单击 "**附加到**" 文本框旁边的 "**选择**"。

     此时将显示 "**选择代码类型**" 对话框。

7. 选择 "**调试以下代码类型**"，然后选择 "**工作流**"。

8. 单击“确定”。

9. 单击 **“附加”** 。

10. 打开浏览器中的默认网页并启动工作流。

## <a name="see-also"></a>请参阅
 [为 Windows Workflow Foundation 调用 Visual Studio 调试器（旧）](../workflow-designer/invoking-the-visual-studio-debugger-for-windows-workflow-foundation-legacy.md) [如何：在工作流中设置断点（旧）](../workflow-designer/how-to-set-breakpoints-in-workflows-legacy.md) [调试旧工作流](../workflow-designer/debugging-legacy-workflows.md)