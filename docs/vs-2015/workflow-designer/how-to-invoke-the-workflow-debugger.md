---
title: 如何：调用工作流调试器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 34c592af-f4f6-4d02-99f6-63a94698e48b
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 34c5cdae4b8730c9058a87061456d5ab6d186c53
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72603670"
---
# <a name="how-to-invoke-the-workflow-debugger"></a>如何：调用工作流调试器
通常，您可以像调试用其他 Visual Studio 编程语言编写的程序那样调试工作流。 可通过以下方法启动工作流调试器：

- 选择 "**调试**" 菜单上的 "**附加到进程**"，为工作流实例选择正在运行的主机进程。 此过程与附加到以托管代码编写的托管进程的过程相同。

- 按**F5**开始运行工作流实例，或者在命中断点后继续运行。

- 使用远程调试。 有关使用远程调试的信息，请参阅[如何：启用远程调试](http://go.microsoft.com/fwlink/?LinkId=196257)。

    > [!NOTE]
    > 如果工作流应用程序针对 x86 体系结构并托管在运行64位操作系统的计算机上，则远程调试将无法工作，除非在远程计算机上安装了 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 或者工作流应用程序的目标更改为**任何 CPU**。

### <a name="stepping-through-code"></a>逐句通过代码

- **单步**执行：可以使用**F11**单步执行活动。 此调试器可以单步执行任何定义的处理程序。 如果未定义处理程序，则可以逐过程执行该活动，或者对于包含其他活动的复合活动，您可以单步执行第一个要执行的活动。

- **跳出：** 你可以使用**Shift-F11**跳出某个活动。 如果跳出某个活动，则会运行当前活动及其所有同级活动，直到这些活动完成为止。 然后调试器将在当前活动的父项处中断。 从代码处理程序中跳出时，调试器将在与此处理程序关联的活动处中断。

- **逐过程**：可以使用**F10**逐过程执行活动。 逐过程执行复合活动时，调试器将在此复合活动的第一个可执行的子活动处中断。 逐过程执行非复合活动（例如 <xref:System.Activities.Statements.Assign> 活动）时，调试器将执行此活动及其关联的处理程序并在下一个活动处中断。 如果执行的活动是复合活动中的最后一个子活动，则在执行之后，调试器将在父活动处中断。

### <a name="debugging-with-f5"></a>用 F5 调试

- 如果要生成工作流控制台应用程序项目，只需按**F5**即可开始调试应用程序和工作流。 如果要生成活动库自身，您必须有可执行的宿主应用程序作为启动项目。 若要在**解决方案资源管理器**中设置启动项目，请右键单击主机的项目名称，然后选择 "**设为启动项目**"。

## <a name="see-also"></a>请参阅
 [如何：在工作流中设置断点](../workflow-designer/how-to-set-breakpoints-in-workflows.md)[调试工作流工作流设计器](../workflow-designer/debugging-workflows-with-the-workflow-designer.md)