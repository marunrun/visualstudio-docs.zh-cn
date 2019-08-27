---
title: 在并行堆栈窗口中查看线程 |Microsoft Docs
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62902262"
---
# <a name="view-threads-and-tasks-in-the-parallel-stacks-window-c-visual-basic-c"></a>在并行堆栈窗口中查看线程和任务 (C#，Visual Basic 中， C++)

**并行堆栈**窗口可用于调试多线程应用程序。 它具有多个视图：

- [线程视图](#threads-view)显示应用程序中的所有线程的都调用堆栈信息。 您可以导航线程之间对这些线程的堆栈帧。

- [任务视图](#tasks-view)显示任务为中心的调用堆栈信息。
  - 在托管代码中，**任务**视图显示的调用堆栈<xref:System.Threading.Tasks.Task?displayProperty=fullName>对象。
  - 在本机代码中，**任务**视图显示的调用堆栈[任务组](/cpp/parallel/concrt/task-parallelism-concurrency-runtime)，[并行算法](/cpp/parallel/concrt/parallel-algorithms)，[异步代理](/cpp/parallel/concrt/asynchronous-agents)，和[轻量级任务](/cpp/parallel/concrt/task-scheduler-concurrency-runtime)。

- [方法视图](#method-view)透视上所选方法的调用堆栈。

## <a name="use-the-parallel-stacks-window"></a>使用“并行堆栈”窗口

若要打开**并行堆栈**窗口中，您必须是在调试会话中。 选择**调试** > **Windows** > **并行堆栈**。

### <a name="toolbar-controls"></a>工具栏控件

**并行堆栈**窗口具有以下工具栏控件：

![在并行堆栈窗口的工具栏](../debugger/media/parallel_stackstoolbar.png "并行堆栈工具栏")

|图标|控件|描述|
|-|-|-|
|![线程/任务组合框](media/parallel_toolbar1.png "线程/任务组合框")|**线程**/**任务**组合框|在线程的调用堆栈和任务的调用堆栈之间切换视图。 有关更多信息，请参见[任务视图](#tasks-view)和[线程视图](#threads-view)。|
|![显示仅标记图标](media/parallel_toolbar2.png "仅显示已标记项图标")|仅显示已标记项|显示仅为如标记在其他调试器窗口中的线程调用堆栈**GPU 线程**窗口和**并行监视**窗口。|
|![切换方法视图图标](media/parallel_toolbar3.png "切换方法视图图标")|切换“方法视图”|调用堆栈视图之间切换和**方法视图**。 有关更多信息，请参见[方法视图](#method-view)。|
|![自动滚动到当前图标](media/parallel_toolbar4.png "自动滚动到当前图标")|自动滚动到当前堆栈帧|自动滚动关系图，以便当前堆栈帧是视图中。 当您从其他窗口，更改当前堆栈帧时或命中大型关系图中的新断点时，此功能非常有用。|
|![切换缩放图标](media/parallel_toolbar5.png "切换缩放图标")|切换缩放控件|显示或隐藏缩放控件窗口的左侧。 <br /><br />无论缩放控件的可见性，还可以缩放通过按**Ctrl**并滚动鼠标滚轮或按**Ctrl**+**Shift** +**+** 放大并**Ctrl**+**Shift** + **-** 若要缩小。 |

### <a name="stack-frame-icons"></a>堆栈帧的图标
以下图标提供有关所有视图中的活动和当前堆栈帧的信息：

|图标|描述|
|-|-|
|![黄色箭头](media/icon_parallelyellowarrow.gif)|指示当前线程的当前位置 （活动堆栈帧）。|
|![线程图标](media/icon_parallelthreads.gif)|指示非当前线程的当前位置 （活动堆栈帧）。|
|![绿色箭头](media/icon_parallelgreenarrow.gif)|指示当前堆栈帧 （当前调试器上下文）。 方法名称为粗体出现的地方。|

### <a name="context-menu-items"></a>上下文菜单项
右键单击中的方法时可用的以下快捷菜单项**线程**视图或**任务**视图。 前六个项是中的相同[调用堆栈窗口](how-to-use-the-call-stack-window.md)。

![在并行堆栈窗口的快捷菜单](../debugger/media/parallel_contmenu.png "并行堆栈窗口中的快捷菜单")

|Menu item|描述|
|-|-|
|**标记**|标记选定项。|
|**取消标记**|取消标记选定项。|
|**冻结**|冻结选定项。|
|**解冻**|解冻选定项。|
|**切换到帧**|中的相应的菜单相同命令**调用堆栈**窗口。 但是，在**并行堆栈**窗口中，一种方法可能在多个帧。 可以在此项的子菜单中选择所需的帧。 如果其中一个堆栈帧位于当前线程上，默认情况下的子菜单中选择该框架。|
|**转到任务**或**转到线程**|切换到**任务**或**线程**视图中，并保留相同堆栈帧突出显示。|
|**转到源代码**|转到源的代码窗口中的相应位置。 |
|**转到反汇编**|转到的相应位置**反汇编**窗口。|
|**显示外部代码**|显示或隐藏外部代码。|
|**十六进制显示**|在十进制和十六进制显示之间切换。|
|**在源中显示线程**|标记源代码窗口中的线程的位置。 |
|**符号加载信息**|此时将打开**符号加载信息**对话框。|
|**符号设置**|此时将打开**符号设置**对话框。 |

## <a name="threads-view"></a>线程视图

在中**线程**查看堆栈帧和蓝色突出显示了当前线程的调用路径。 由黄色箭头显示当前线程的位置。

若要更改当前堆栈帧，请双击另一种方法。 这可能会切换当前线程，具体取决于你选择的方法是否是当前线程或另一个线程的一部分。

当**线程**视图关系图是太大，无法适应窗口，**鸟瞰**控件显示在窗口中。 控件可以导航到的关系图的不同部分中，可以移动框架。

下图显示了一个线程从 Main 进入本机代码转换到托管的。 六个线程都在当前方法。 一个将继续执行到 Thread.Sleep，并且另一个将继续到 Console.WriteLine，再到 SyncTextWriter.WriteLine。

 ![线程并行堆栈窗口中的视图](../debugger/media/parallel_stack1.png "线程并行堆栈窗口中的视图")

下表介绍的主要功能**线程**视图：

|标注|元素名称|描述|
|-|-|-|
|1|调用堆栈段或节点|包含一系列的一个或多个线程的方法。 如果帧没有连接到该箭头线，框架将显示线程的整个调用路径。|
|2|蓝色突出显示|指示当前线程的调用路径。|
|3|箭头线|连接节点，以组成线程的整个调用路径。|
|4|节点标头|显示进程和线程的节点的数目。|
|5|方法|表示同一方法中的一个或多个堆栈帧。|
|6|在方法上的工具提示|当悬停在一个方法时出现。 在中**线程**视图中，工具提示显示所有线程，类似于表中**线程**窗口。 |

## <a name="tasks-view"></a>任务视图
如果您的应用程序使用<xref:System.Threading.Tasks.Task?displayProperty=fullName>对象 （托管代码） 或`task_handle`对象 （本机代码） 来表示并行度，则可以使用**任务**视图。 “任务”视图显示任务（而不是线程）的调用堆栈。

在中**任务**视图：

- 不会运行任务的线程的调用堆栈不会显示。
- 运行任务的线程的调用堆栈直观地修整的顶部和底部，以显示任务的相关度最高帧中。
- 一个线程上多个任务时，这些任务的调用堆栈显示在单独的节点。

若要查看整个调用堆栈，切换回**线程**视图中的堆栈帧中右键单击并选择**转到线程**。

如下图所示**线程**顶部和相应的视图**任务**视图底部。

![线程和任务视图](../debugger/media/parallel_threads-tasks.png "线程和任务视图")

将鼠标悬停显示带有其他信息的工具提示的方法。 在中**任务**视图中，工具提示会显示所有任务在表中类似于**任务**窗口。

下图显示了中的方法的工具提示**线程**视图顶部和相应**任务**视图底部。

![线程和任务的工具提示](../debugger/media/parallel_threads-tasks-tooltips.png "线程和任务的工具提示")

## <a name="method-view"></a>方法视图
眖**线程**视图或**任务**视图中，您可以通过选择透视关系图上的当前方法**切换方法视图**工具栏上的图标。 “方法视图”非常清晰地显示了调用当前方法或被当前方法调用的所有线程上的所有方法。 下图显示了相同的信息的外观**线程**查看左侧，并在**方法视图**在右侧。

![线程视图和方法视图](../debugger/media/parallel_methodview.png "线程视图和方法视图")

如果您切换到新的堆栈帧，您会使该方法成为当前方法，并**方法视图**显示所有调用方和被调用方用于新的方法。 这可能会导致某些线程显示在视图中或从视图中消失，具体取决于线程的调用堆栈上是否显示该方法。 若要返回到调用堆栈视图，请选择**方法视图**再次工具栏图标。

## <a name="see-also"></a>请参阅
- [开始调试多线程应用程序](../debugger/get-started-debugging-multithreaded-apps.md)
- [演练：调试并行应用程序](../debugger/walkthrough-debugging-a-parallel-application.md)
- [初探调试器](../debugger/debugger-feature-tour.md)
- [调试托管代码](../debugger/debugging-managed-code.md)
- [并行编程](/dotnet/standard/parallel-programming/index)
- [使用“任务”窗口](../debugger/using-the-tasks-window.md)
- [Task 类](../extensibility/debugger/task-class-internal-members.md)
