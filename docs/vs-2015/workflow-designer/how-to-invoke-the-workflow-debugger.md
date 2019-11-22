---
title: 'How to: Invoke the Workflow Debugger | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 34c592af-f4f6-4d02-99f6-63a94698e48b
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 13fd54eeebf0323fcb9b8cad6a8cd8b75ae11fb3
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74292896"
---
# <a name="how-to-invoke-the-workflow-debugger"></a>如何：调用工作流调试器
通常，您可以像调试用其他 Visual Studio 编程语言编写的程序那样调试工作流。 可通过以下方法启动工作流调试器：

- Select **Attach to Process** on the **Debug** menu to select the running host process for your workflow instance. 此过程与附加到以托管代码编写的托管进程的过程相同。

- Press **F5** to start running an instance of the workflow, or to continue to run after a breakpoint has been hit.

- 使用远程调试。 For information on using remote debugging, see [How to: Enable Remote Debugging](https://go.microsoft.com/fwlink/?LinkId=196257).

    > [!NOTE]
    > If the workflow application targets the x86 architecture and is hosted on a machine running a 64 bit operating system, then remote debugging will not work unless [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] is installed on the remote machine or the target for the workflow application is changed to **Any CPU**.

### <a name="stepping-through-code"></a>逐句通过代码

- **Step In**: You can step into an activity using **F11**. 此调试器可以单步执行任何定义的处理程序。 如果未定义处理程序，则可以逐过程执行该活动，或者对于包含其他活动的复合活动，您可以单步执行第一个要执行的活动。

- **Step Out:** You can step out of an activity using **Shift-F11**. 如果跳出某个活动，则会运行当前活动及其所有同级活动，直到这些活动完成为止。 然后调试器将在当前活动的父项处中断。 从代码处理程序中跳出时，调试器将在与此处理程序关联的活动处中断。

- **Step Over**: You can step over an activity using **F10**. 逐过程执行复合活动时，调试器将在此复合活动的第一个可执行的子活动处中断。 逐过程执行非复合活动（例如 <xref:System.Activities.Statements.Assign> 活动）时，调试器将执行此活动及其关联的处理程序并在下一个活动处中断。 如果执行的活动是复合活动中的最后一个子活动，则在执行之后，调试器将在父活动处中断。

### <a name="debugging-with-f5"></a>用 F5 调试

- If you are building a Workflow Console Application project, simply press **F5** to begin debugging into your application and workflow. 如果要生成活动库自身，您必须有可执行的宿主应用程序作为启动项目。 To set a startup project in **Solution Explorer**, right-click the project name of the host and select **Set as StartUp Project**.

## <a name="see-also"></a>请参阅
 [How to: Set Breakpoints in Workflows](../workflow-designer/how-to-set-breakpoints-in-workflows.md) [Debugging Workflows with the Workflow Designer](../workflow-designer/debugging-workflows-with-the-workflow-designer.md)