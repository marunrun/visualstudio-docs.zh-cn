---
title: 使用 "并行堆栈" 窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.parallelstacks
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, parallel tasks window
ms.assetid: f50efb78-5206-4803-bb42-426ef8133f2f
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e89125c8e1dea25ab02fe64c21b8166e9d65194a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542215"
---
# <a name="using-the-parallel-stacks-window"></a>使用“并行堆栈”窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

调试多线程应用程序时，"**并行堆栈**" 窗口很有用。 其 "**线程" 视图**显示应用程序中所有线程的调用堆栈信息。 使用该视图可以在线程和这些线程上的堆栈帧之间进行导航。 在托管代码中，"**任务" 视图**显示对象的调用堆栈 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 。 在本机代码中，"**任务" 视图**显示[任务组](https://msdn.microsoft.com/library/42f05ac3-2098-494a-ba84-737fcdcad077)、[并行算法](https://msdn.microsoft.com/library/045dca7b-4d73-4558-a44c-383b88a28473)、[异步代理](https://msdn.microsoft.com/library/6cf6ccc6-87f1-4e14-af15-ea8ba58fef1a)和[轻量级任务](https://msdn.microsoft.com/library/9aba278c-e0c9-4ede-b7c6-fedf7a365d90)的调用堆栈。  
  
## <a name="threads-view"></a>线程视图  
 下图演示的一个线程从 Main 执行到 A 再执行到 B，然后执行到某个外部代码。 其余两个线程从某个外部代码开始，执行到 A，但其中一个线程继续执行到 B，然后执行到某个外部代码，而另一个线程继续执行到 C，然后执行到某个 AnonymousMethod。  
  
 ![“并行堆栈”窗口中的“线程”视图](../debugger/media/parallel-stacksthread.png "Parallel_StacksThread")  
  
 在图示中，当前线程的调用路径突出显示为蓝色，活动堆栈帧由黄色箭头表示。 您可以通过在 "**并行堆栈**" 窗口中选择其他方法来更改当前堆栈帧。 这也可能导致切换当前线程，具体取决于所选方法是当前线程的一部分还是属于其他线程。 下表描述了 "**并行堆栈**" 窗口的主要功能，如图所示。  
  
|标注字母|元素名称|说明|  
|--------------------|------------------|-----------------|  
|A|调用堆栈段或节点|包含一个或多个线程的一系列方法上下文。 如果该节点没有连接箭头线，则表示线程的整个调用路径。|  
|B|蓝色突出显示|指示当前线程的调用路径。|  
|C|箭头线|连接节点，以组成线程的整个调用路径。|  
|D|节点标头上的工具提示|显示其调用路径共享此节点的每个线程的 ID 和用户定义名称。|  
|E|方法上下文|表示同一方法中的一个或多个堆栈帧。|  
|F|方法上下文上的工具提示|在 "线程" 视图中，它会显示与 "**线程**" 窗口类似的表中的所有线程。 在任务视图中，它会显示与 "**并行任务**" 窗口类似的表中的所有任务。|  
  
 此外，当图表太大而无法放入窗口时，"并行堆栈" 窗口将在主窗格中显示**鸟瞰**图图标。 单击该图标可在窗口中查看整个关系图。  
  
## <a name="method-context-icons"></a>方法上下文图标  
 下表介绍了提供有关活动堆栈帧和当前堆栈帧的信息的图标：  
  
|图标|描述|  
|-|-|
|![并行堆栈黄色箭头](../debugger/media/icon-parallelyellowarrow.gif "Icon_ParallelYellowArrow")|指示方法上下文包含当前线程的活动堆栈帧。|  
|![“并行堆栈线程”图标](../debugger/media/icon-parallelthreads.gif "Icon_ParallelThreads")|指示方法上下文包含非当前线程的活动堆栈帧。|  
|![并行堆栈绿色箭头](../debugger/media/icon-parallelgreenarrow.gif "Icon_ParallelGreenArrow")|指示方法上下文包含当前堆栈帧。 该方法名称在其所在的所有节点中都以粗体显示。|  
  
## <a name="toolbar-controls"></a>工具栏控件  
 下面的图和表介绍“并行堆栈”工具栏中提供的控件。  
  
 ![“并行堆栈”窗口中的工具栏](../debugger/media/parallel-stackstoolbar.png "Parallel_StacksToolbar")  
  
|标注字母|控件|说明|  
|--------------------|-------------|-----------------|  
|A|线程/任务组合框|在线程的调用堆栈和任务的调用堆栈之间切换视图。 有关更多信息，请参见“任务视图”和“线程视图”。|  
|B|仅显示已标记项|仅显示在其他调试窗口中标记的线程的调用堆栈，如 " **GPU 线程**" 窗口和 "**并行监视**" 窗口。|  
|C|切换方法视图|在堆栈视图和方法视图之间切换。 有关更多信息，请参见“方法视图”。|  
|D|自动滚动到当前堆栈帧|自动滚动关系图，以便能够看到当前堆栈帧。 当您从其他窗口更改当前堆栈帧或在大型关系图中命中新断点时，此功能非常有用。|  
|E|切换缩放控件|显示或隐藏缩放控件。 您还可以通过按 CTRL 并滚动鼠标滚轮来进行缩放，而不考虑缩放控件的可见性，或使用**ctrl + shift + "+"** 进行放大，按**ctrl + shift + "-"** 缩小。按**CTRL + F8**将缩放以适合屏幕大小。|  
  
### <a name="context-menu-items"></a>上下文菜单项  
 下面的图和表介绍在线程视图或任务视图中右击方法上下文时可用的快捷菜单项。 最后六项直接从“调用堆栈”窗口借用而来，并没有引入新行为。  
  
 ![“并行堆栈”窗口中的快捷菜单](../debugger/media/parallel-contmenu.png "Parallel_ContMenu")  
  
|菜单项|说明|  
|---------------|-----------------|  
|标志|标记选定项。|  
|取消标记|取消标记选定项。|  
|冻结|冻结选定项。|  
|解冻|解冻选定项。|  
|转到任务（线程）|与工具栏上的对应组合框执行相同的功能，但突出显示同一堆栈帧。|  
|转到源代码|导航到源代码中与用户右击的堆栈帧对应的位置。|  
|切换到帧|与“调用堆栈”窗口上的对应菜单命令相同。 但是，使用并行堆栈时，多个帧可能与一个方法上下文相对应。 因此，该菜单项具有子菜单，每个子菜单表示一个特定堆栈帧。 如果其中一个堆栈帧位于当前线程上，将选中与该堆栈帧对应的菜单。|  
|转到反汇编|导航到反汇编窗口中与用户右击的堆栈帧对应的位置。|  
|显示外部代码|显示或隐藏外部代码。|  
|十六进制显示|在十进制和十六进制显示之间切换。|  
|符号加载信息|显示相应的对话框。|  
|符号设置|显示相应的对话框。|  
  
## <a name="tasks-view"></a>任务视图  
 如果你的应用程序使用 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 对象（托管代码）或 `task_handle` 对象（本机代码）来表示并行，则可以使用 "并行堆栈" 窗口工具栏中的组合框来切换到*任务视图*。 任务视图显示任务（而不是线程）的调用堆栈。 任务视图与线程视图不同，如下所示：  
  
- 不显示未运行任务的线程的调用堆栈。  
  
- 在顶部和底部对运行任务的线程的调用堆栈进行直观的修剪，以便显示与任务关系最密切的帧。  
  
- 当一个线程上有多个任务时，会将这些任务的调用堆栈拆分为单独的节点。  
  
  下图右侧显示的是并行堆栈任务视图，左侧显示的是对应的线程视图。  
  
  ![“并行堆栈”窗口中的“任务”视图](../debugger/media/parallel-tasksview.png "Parallel_TasksView")  
  
  若要查看整个调用堆栈，只需右键单击堆栈帧，然后单击 "**转到线程**" 即可切换回 "线程" 视图。  
  
  如上表所述，将鼠标指针悬停在方法上下文的上方，即可看到附加信息。 下图显示了线程视图和任务视图的工具提示中的信息。  
  
  ![“并行堆栈”窗口中的工具提示](../debugger/media/parallel-stack-tooltips.png "Parallel_Stack_Tooltips")  
  
## <a name="method-view"></a>方法视图  
 在线程视图或任务视图中，可以通过单击工具栏上的“方法视图”图标，以当前方法为中心显示图形。 方法视图非常清晰地显示了调用当前方法或被当前方法调用的所有线程上的所有方法。 下图显示了一个线程视图，以及同样的信息在方法视图中的显示情况。  
  
 ![“并行堆栈”窗口中的方法视图](../debugger/media/parallel-methodview.png "Parallel_MethodView")  
  
 通过切换到新堆栈帧，可使该方法成为当前方法，并在窗口中显示新方法的所有调用方和被调用方。 这可能会导致某些线程显示在视图中或从视图中消失，具体取决于线程的调用堆栈上是否显示该方法。 若要返回堆栈视图，请再次单击“方法视图”工具栏按钮。  
  
## <a name="see-also"></a>另请参阅  
 [演练：调试并行应用程序](../debugger/walkthrough-debugging-a-parallel-application.md)   
 [调试器基础知识](../debugger/debugger-basics.md)   
 [调试托管代码](../debugger/debugging-managed-code.md)   
 [并行编程](https://msdn.microsoft.com/library/4d83c690-ad2d-489e-a2e0-b85b898a672d)   
 [使用 "任务" 窗口](../debugger/using-the-tasks-window.md)   
 [演练：调试并行应用程序](../debugger/walkthrough-debugging-a-parallel-application.md)   
 [Task 类](../extensibility/debugger/task-class-internal-members.md)
