---
title: 在“并行堆栈”窗口中查看线程 | Microsoft Docs
ms.date: 11/20/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.parallelstacks
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, parallel tasks window
ms.assetid: f50efb78-5206-4803-bb42-426ef8133f2f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e9728346bc4c6d805bb0febd3a0d5bef0ed809a5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62902262"
---
# <a name="view-threads-and-tasks-in-the-parallel-stacks-window-c-visual-basic-c"></a>在“并行堆栈”窗口中查看线程和任务（C#、Visual Basic 和 C++）

调试多线程应用程序时，“并行堆栈”窗口非常有用。 它有多个视图：

- [“线程”视图](#threads-view)显示应用中所有线程的调用堆栈信息。 可以在线程和这些线程上的堆栈帧之间进行导航。

- [任务视图](#tasks-view)显示以任务为中心的调用堆栈信息。
  - 在托管代码中，“任务”视图示 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 对象的调用堆栈。
  - 在本机代码中，“任务”视图显示[任务组](/cpp/parallel/concrt/task-parallelism-concurrency-runtime)、[并行算法](/cpp/parallel/concrt/parallel-algorithms)、[异步代理](/cpp/parallel/concrt/asynchronous-agents)和[轻量级任务](/cpp/parallel/concrt/task-scheduler-concurrency-runtime)的调用堆栈。

- [方法视图](#method-view)以选定方法为中心显示调用堆栈。

## <a name="use-the-parallel-stacks-window"></a>使用“并行堆栈”窗口

只能在调试会话中打开“并行堆栈”窗口。 选择“调试” > “窗口” > “并行堆栈”  。

### <a name="toolbar-controls"></a>工具栏控件

“并行堆栈”窗口具有以下工具栏控件：

![“并行堆栈”窗口中的工具栏](../debugger/media/parallel_stackstoolbar.png "“并行堆栈”工具栏")

|图标|控件|描述|
|-|-|-|
|![线程/任务组合框](media/parallel_toolbar1.png "Threads/Tasks combo box")|线程/任务组合框 |在线程的调用堆栈和任务的调用堆栈之间切换视图。 有关更多信息，请参见[任务视图](#tasks-view)和[线程视图](#threads-view)。|
|![“仅显示已标记项”图标](media/parallel_toolbar2.png "Show Only Flagged icon")|仅显示已标记项|仅显示在其他调试器窗口（如“GPU 线程”窗口和“并行监视”窗口）中已标记的线程的调用堆栈 。|
|![“切换方法视图”图标](media/parallel_toolbar3.png "Toggle Method View icon")|切换“方法视图”|在调用堆栈视图和方法视图之间切换。 有关更多信息，请参见[方法视图](#method-view)。|
|![“自动滚动到当前”图标](media/parallel_toolbar4.png "Auto Scroll to Current icon")|自动滚动到当前堆栈帧|自动滚动关系图，以便能够看到当前堆栈帧。 当从其他窗口更改当前堆栈帧或在大型关系图中命中新断点时，此功能非常有用。|
|![“切换缩放”图标](media/parallel_toolbar5.png "Toggle Zoom icon")|切换缩放控件|显示或隐藏窗口左侧的缩放控件。 <br /><br />无论缩放控件是否可见，都可以通过按 Ctrl 并滚动鼠标滚轮来进行缩放，或者按 Ctrl+Shift++ 放大，按 Ctrl+Shift+- 缩小      。 |

### <a name="stack-frame-icons"></a>堆栈帧图标
以下图标提供有关所有视图中活动堆栈帧和当前堆栈帧的信息：

|图标|描述|
|-|-|
|![黄色箭头](media/icon_parallelyellowarrow.gif)|指示当前线程的当前位置（活动堆栈帧）。|
|![“线程”图标](media/icon_parallelthreads.gif)|指示非当前线程的当前位置（活动堆栈帧）。|
|![绿色箭头](media/icon_parallelgreenarrow.gif)|指示当前堆栈帧（当前调试器上下文）。 方法名称在任何地方都显示为粗体。|

### <a name="context-menu-items"></a>上下文菜单项
在“线程”视图或“任务”视图中右键单击方法时，可以看到以下快捷菜单项 。 最后六项与[“调用堆栈”窗口](how-to-use-the-call-stack-window.md)中的相同。

![“并行堆栈”窗口中的快捷菜单](../debugger/media/parallel_contmenu.png "Shortcut menu in Parallel Stacks window")

|Menu item|描述|
|-|-|
|**标记**|标记选定项。|
|**取消标记**|取消标记选定项。|
|**冻结**|冻结选定项。|
|**解冻**|解冻选定项。|
|**切换到帧**|与“调用堆栈”窗口上的对应菜单命令相同。 但是在“并行堆栈”窗口中，一个方法可能位于多个帧中。 可以在此项的子菜单中选择所需的帧。 如果堆栈帧中有一个位于当前线程上，则子菜单中会默认选中该帧。|
|“转到任务”或“转到线程” |切换到“任务”或“线程”视图，并突出显示相同的堆栈帧 。|
|**转到源代码**|转到源代码窗口中的相应位置。 |
|**转到反汇编**|转到“反汇编”窗口中的相应位置。|
|**显示外部代码**|显示或隐藏外部代码。|
|**十六进制显示**|在十进制和十六进制显示之间切换。|
|**在源中显示线程**|标记线程在源代码窗口中的位置。 |
|**符号加载信息**|打开“符号加载信息”对话框。|
|**符号设置**|打开“符号设置”对话框。 |

## <a name="threads-view"></a>线程视图

在“线程”视图中，当前线程的堆栈帧和调用路径突出显示为蓝色。 线程的当前位置由黄色箭头显示。

若要更改当前堆栈帧，请双击其他方法。 这也可能会切换当前线程，具体取决于所选的方法属于当前线程还是其他线程。

当“线程”视图关系图太大而无法放入窗口时，窗口中会出现“鸟瞰视图”控件 。 你可以在该控件中移动帧以导航到关系图的不同部分。

下图演示的是一个执行从主代码到托管代码再到本机代码的代码转换的线程。 当前方法中包含六个线程。 一个继续运行到 Thread.Sleep，另一个继续运行到 Console.WriteLine 再运行到 SyncTextWriter.WriteLine。

 ![“并行堆栈”窗口中的“线程”视图](../debugger/media/parallel_stack1.png "Threads view in Parallel Stacks window")

下表介绍“线程”视图的主要功能：

|标注|元素名称|描述|
|-|-|-|
|1|调用堆栈段或节点|包含一个或多个线程的一系列方法。 如果该帧没有连接箭头线，则该帧显示线程的整个调用路径。|
|2|蓝色突出显示|指示当前线程的调用路径。|
|3|箭头线|连接节点，以组成线程的整个调用路径。|
|4|节点标头|显示节点的进程数和线程数。|
|5|方法|表示同一方法中的一个或多个堆栈帧。|
|6|方法上的工具提示|在将鼠标悬停在方法上时显示。 在“线程”视图中，工具提示会在类似“线程”窗口的表中显示所有线程 。 |

## <a name="tasks-view"></a>任务视图
如果应用使用 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 对象（托管代码）或 `task_handle` 对象（本机代码）来表示并行，则可以使用“任务”视图。 “任务”视图显示任务（而不是线程）的调用堆栈。

在“任务”视图中：

- 不显示运行中任务以外的线程的调用堆栈。
- 身为运行中任务的线程，其调用堆栈的首尾将被隐藏，以显示与任务关系最密切的帧。
- 当一个线程上有多个任务时，会在单独的节点中显示这些任务的调用堆栈。

若要查看整个调用堆栈，请右键单击堆栈帧并选择“转到线程”以切换回“线程”视图 。

下图顶部显示的是“线程”视图，底部显示的是对应的“任务”视图 。

![“线程”视图和“任务”视图](../debugger/media/parallel_threads-tasks.png "Threads and Tasks views")

将鼠标悬停在方法上可显示带有额外信息的工具提示。 在“任务”视图中，工具提示会在类似于“任务”窗口的表中显示所有任务 。

下图顶部显示的是“线程”视图中的方法的工具提示，底部显示的是对应的“任务”视图的工具提示 。

![“线程”和“任务”工具提示](../debugger/media/parallel_threads-tasks-tooltips.png "Threads and Tasks tooltips")

## <a name="method-view"></a>方法视图
在“线程”视图或“任务”视图中，可以通过选择工具栏上的“切换方法视图”图标，以当前方法为中心显示图形  。 “方法视图”非常清晰地显示了调用当前方法或被当前方法调用的所有线程上的所有方法。 下图在左侧和右侧分别显示了相同的信息在“线程”视图和“方法视图”中的显示情况 。

![“线程”视图和“方法视图”](../debugger/media/parallel_methodview.png "Threads view and Method View")

通过切换到新堆栈帧，可使该方法成为当前方法，并在“方法视图”中显示这个新方法的所有调用方和被调用方。 这可能会导致某些线程显示在视图中或从视图中消失，具体取决于线程的调用堆栈上是否显示该方法。 若要返回调用堆栈视图，请再次选择“方法视图”工具栏图标。

## <a name="see-also"></a>请参阅
- [开始调试多线程应用程序](../debugger/get-started-debugging-multithreaded-apps.md)
- [演练：调试并行应用程序](../debugger/walkthrough-debugging-a-parallel-application.md)
- [初探调试器](../debugger/debugger-feature-tour.md)
- [调试托管代码](../debugger/debugging-managed-code.md)
- [并行编程](/dotnet/standard/parallel-programming/index)
- [使用“任务”窗口](../debugger/using-the-tasks-window.md)
- [Task 类](../extensibility/debugger/task-class-internal-members.md)
