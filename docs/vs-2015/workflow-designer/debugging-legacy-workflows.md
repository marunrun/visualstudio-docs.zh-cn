---
title: 调试旧工作流 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- workflows, debugging
- debugging, workflows
- debugging workflows
ms.assetid: e6097b47-760a-4b30-a92c-ae70cdbda49f
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 40ae0a08e1623e1b90046d164d8bfe04eaf67229
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656864"
---
# <a name="debugging-legacy-workflows"></a>调试旧版工作流
如果要用 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 中的传统 [!INCLUDE[vs_current_long](../includes/vs-current-long-md.md)] 构建面向 .NET Framework 3.0 或 3.5 的 [!INCLUDE[wf](../includes/wf-md.md)] 应用程序，可以像对其他程序一样，通过设置断点、附加到进程、检查线程和调用堆栈来调试工作流。 您还可以选择远程调试。

> [!NOTE]
> 如果计算机上安装并卸载过 Visual Studio 的多个版本，在以下两种情况下 WF3 调试可能失败：
>
> - 设置的断点未命中。
>   - 将显示以下消息：
>
>   **无法在 web 服务器上启动调试。调试程序安装不正确。 无法调试请求的代码类型。 运行安装程序以安装或修复调试器。**
>
>   如果在调试 .NET Framework 3.0 或 3.5 工作流时发生以上任一情况，请对 Visual Studio 安装进行修复。

 [!INCLUDE[wf2](../includes/wf2-md.md)] 集成具有以下标准 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 调试窗口：

- **断点**：按预期方式工作，但指定了函数名称的活动。

- **调用堆栈**：经过修改，可提供已在工作流实例中执行的活动的大纲。 " **调用堆栈** " 窗口中的条目是执行活动的深度优先搜索。 您可以双击某个项以将焦点放在选定的活动上。

- **线程**：提供正在调试的工作流实例的实例 ID。

  Visual Studio for Windows Workflow Foundation 不支持以下调试功能：

- 设计器图面上的条件断点。

- 快速监视。

- 设置下一语句。

- 运行到光标处。

- 编辑并继续。

- 实时调试。

- 混合模式调试。

## <a name="in-this-section"></a>本节内容
 [调用 Visual Studio Debugger for Windows Workflow Foundation（旧版）](../workflow-designer/invoking-the-visual-studio-debugger-for-windows-workflow-foundation-legacy.md)

 [禁用 Visual Studio Debugger for Windows Workflow Foundation（旧版）](../workflow-designer/disabling-the-visual-studio-debugger-for-windows-workflow-foundation-legacy.md)

 [如何：调试基于 ASP.NET 的工作流（旧版）](../workflow-designer/how-to-debug-aspnet-based-workflows-legacy.md)

 [如何：在工作流中设置断点（旧版）](../workflow-designer/how-to-set-breakpoints-in-workflows-legacy.md)

 [通过远程计算机调试工作流（旧版）](../workflow-designer/debugging-workflows-from-a-remote-computer-legacy.md)

 [调试单步执行选项（旧版）](../workflow-designer/debug-stepping-options-legacy.md)

 [如何：更改调试单步执行选项（旧版）](../workflow-designer/how-to-change-the-debug-stepping-option-legacy.md)