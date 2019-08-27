---
title: 使用工作流设计器调试工作流
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Workflow Designer [WFD], debugging workflows
- Workflow Designer [WFD], debugging workflows
ms.assetid: d71308cf-d464-4536-8711-0d0a8eadb255
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1270e57ae6c9235311569c04ebb982157ea3b608
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62949742"
---
# <a name="debug-workflows-with-the-workflow-designer"></a>调试工作流与工作流设计器

**工作流设计器**提供调试工作流和自定义活动的能力。 过程和行为类似于默认 Visual Studio 调试器。

## <a name="invoke-the-workflow-debugger"></a>调用工作流调试器

通常，您可以像调试用其他 Visual Studio 编程语言编写的程序那样调试工作流。 可通过以下方法启动工作流调试器：

- 选择**附加到进程**上**调试**菜单中进行选择的工作流实例正在运行的主机进程。 此过程与附加到以托管代码编写的托管进程的过程相同。

- 按**F5**以开始运行的工作流实例，或者以命中断点后继续运行。

- 使用远程调试。 有关使用远程调试的信息，请参阅[如何：启用远程调试](/previous-versions/visualstudio/visual-studio-2010/febz73k0(v=vs.100))。

   > [!NOTE]
   > 如果工作流应用程序针对 x86 体系结构并位于运行 64 位操作系统的计算机上远程调试不会工作，除非在远程计算机上安装 Visual Studio 或工作流应用程序的目标更改为**任何 CPU**。

## <a name="step-through-code"></a>逐行执行代码

- **中的步骤**:通过按到活动步骤**F11**。 此调试器可以单步执行任何定义的处理程序。 如果未定义处理程序，则可以逐过程执行该活动，或者对于包含其他活动的复合活动，您可以单步执行第一个要执行的活动。

- **跳出：** 通过按跳出某个活动**Shift**+**F11**。 如果跳出某个活动，则会运行当前活动及其所有同级活动，直到这些活动完成为止。 然后调试器将在当前活动的父项处中断。 从代码处理程序中跳出时，调试器将在与此处理程序关联的活动处中断。

- **逐过程执行**:逐过程执行某个活动通过按**F10**。 逐过程执行复合活动时，调试器将在此复合活动的第一个可执行的子活动处中断。 逐过程执行非复合活动（例如 <xref:System.Activities.Statements.Assign> 活动）时，调试器将执行此活动及其关联的处理程序并在下一个活动处中断。 如果执行的活动是复合活动中的最后一个子活动，则在执行之后，调试器将在父活动处中断。

## <a name="debug-with-f5"></a>使用 F5 进行调试

如果您正在构建的工作流控制台应用，只需按**F5**开始调试应用程序和工作流。 如果要自己生成活动库，则必须指定为启动项目的可执行的主机应用程序。 若要在中设置启动项目**解决方案资源管理器**，右键单击项目名称的主机，然后选择**设为启动项目**。