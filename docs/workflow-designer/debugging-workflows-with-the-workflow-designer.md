---
title: 使用工作流设计器调试工作流
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Workflow Designer [WFD], debugging workflows
- Workflow Designer [WFD], debugging workflows
ms.assetid: d71308cf-d464-4536-8711-0d0a8eadb255
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4b8de1ff9875d175c956a45b87d459d0943e783c
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75597056"
---
# <a name="debug-workflows-with-the-workflow-designer"></a>用工作流设计器调试工作流

**工作流设计器**提供调试工作流和自定义活动的功能。 进程和行为类似于默认 Visual Studio 调试器。

## <a name="invoke-the-workflow-debugger"></a>调用工作流调试器

通常，您可以像调试用其他 Visual Studio 编程语言编写的程序那样调试工作流。 可通过以下方法启动工作流调试器：

- 选择 "**调试**" 菜单上的 "**附加到进程**"，为工作流实例选择正在运行的主机进程。 此过程与附加到以托管代码编写的托管进程的过程相同。

- 按**F5**开始运行工作流实例，或者在命中断点后继续运行。

- 使用远程调试。 有关使用远程调试的信息，请参阅[如何：启用远程调试](/previous-versions/visualstudio/visual-studio-2010/febz73k0(v=vs.100))。

   > [!NOTE]
   > 如果工作流应用程序针对 x86 体系结构并托管在运行64位操作系统的计算机上，则除非远程计算机上安装了 Visual Studio，否则远程调试将不起作用，或将工作流应用程序的目标更改为 "**任意 CPU**"。

## <a name="step-through-code"></a>逐行执行代码

- **单步**执行：按**F11**单步执行活动。 此调试器可以单步执行任何定义的处理程序。 如果未定义处理程序，则可以逐过程执行该活动，或者对于包含其他活动的复合活动，您可以单步执行第一个要执行的活动。

- **跳出：** 按**Shift**+**F11**跳出活动。 如果跳出某个活动，则会运行当前活动及其所有同级活动，直到这些活动完成为止。 然后调试器将在当前活动的父项处中断。 从代码处理程序中跳出时，调试器将在与此处理程序关联的活动处中断。

- **逐过程**：按**F10**逐过程执行活动。 逐过程执行复合活动时，调试器将在此复合活动的第一个可执行的子活动处中断。 逐过程执行非复合活动（例如 <xref:System.Activities.Statements.Assign> 活动）时，调试器将执行此活动及其关联的处理程序并在下一个活动处中断。 如果执行的活动是复合活动中的最后一个子活动，则在执行之后，调试器将在父活动处中断。

## <a name="debug-with-f5"></a>用 F5 调试

如果要生成工作流控制台应用，只需按**F5**即可开始调试应用程序和工作流。 如果要自行生成活动库，则必须指定可执行的主机应用程序作为启动项目。 若要在**解决方案资源管理器**中设置启动项目，请右键单击主机的项目名称，然后选择 "**设为启动项目**"。
