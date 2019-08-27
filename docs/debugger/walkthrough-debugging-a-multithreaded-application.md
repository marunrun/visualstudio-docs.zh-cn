---
title: 在调试器中查看线程 |Microsoft Docs
ms.date: 10/29/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.threads
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- threading [Visual Studio], debugging
- Thread.Name property
- debugger, Threads window
- SetThreadName function
- Threads window
- '@TIB'
- debugging [Visual Studio], threads
ms.assetid: 590ffd57-0556-43d8-8962-ee27e5b2b7d7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4f65bd7a904f30f132f654b6dd718532d9d0e66e
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67821591"
---
# <a name="view-threads-in-the-visual-studio-debugger-by-using-the-threads-window-c-visual-basic-c"></a>通过使用线程窗口在 Visual Studio 调试器中查看的主题 (C#，Visual Basic 中， C++)
在中**线程**窗口中，您可以检查和使用的线程中进行调试的应用程序。 有关如何使用的分步指导**线程**窗口中，请参阅[演练：使用线程窗口调试](../debugger/how-to-use-the-threads-window.md)。

## <a name="use-the-threads-window"></a>使用“线程”窗口
 **线程**窗口包含其中每行描述一个单独的线程在应用程序中的表。 默认情况下，该表列出应用程序中的所有线程，但可以筛选列表以仅显示感兴趣的线程。 每个列说明了不同类型的信息。 您还可以隐藏某些列。 如果显示所有列，显示以下各列，从左到右：

- **标志**:在此未标记的专栏中，可以标记要特别注意的线程。 有关如何标记一个线程的信息，请参阅[如何：标记线程和取消标记线程](../debugger/how-to-flag-and-unflag-threads.md)。

- **当前线程**:在此未标记的列，黄色箭头指示当前线程。 概述箭头指示非当前线程的当前调试器上下文。

- **ID**:显示每个线程的标识号。

- **托管 ID**:显示托管线程的托管的标识号。

- **类别**:显示为用户界面线程、 远程过程调用处理程序或工作线程的线程的类别。 一个特殊类别标识应用程序的主线程。

- **名称**:如果有的话，或按名称标识每个线程\<无名称 >。

- **位置**:显示线程正在其中运行。 可以展开此位置以显示线程的完整调用堆栈。

- **优先级**:（默认情况下隐藏） 的高级的列，显示系统已分配给每个线程的优先级。

- **关联掩码**:高级的列 （默认情况下隐藏），显示了每个线程的处理器关联掩码。 在多处理器系统中，关联掩码确定线程可以在哪些处理器上运行。

- **挂起项计数**:高级的列 （默认情况下隐藏），显示挂起项计数。 此计数确定线程是否可以运行。 有关挂起计数的详细信息，请参阅[冻结和解冻线程](#freeze-and-thaw-threads)。

- **进程名称**:（默认情况下隐藏） 的高级的列，显示每个线程所属的进程。 在调试多个进程时，此列中的数据很有用。

- **进程 ID**:（默认情况下隐藏） 的高级的列，显示每个线程所属的进程 ID。

- **传输限定符**:高级的列 （默认情况下隐藏） 唯一标识调试器连接到的计算机。

### <a name="to-display-the-threads-window-in-break-mode-or-run-mode"></a>以中断模式或运行模式显示“线程”窗口

- 当 Visual Studio 在调试模式下，选择**调试**菜单，依次指向**Windows**，然后选择**线程**。

### <a name="to-display-or-hide-a-column"></a>显示或隐藏列

- 在顶部的工具栏**线程**窗口中，选择**列**。 然后，选中或清除要显示或隐藏的列的名称。

## <a name="display-flagged-threads"></a>显示标记的线程
 在“线程”窗口中，可以用图标标记来标记要格外关注的线程  。 有关详细信息，请参阅[如何：标记线程和取消标记线程](../debugger/how-to-flag-and-unflag-threads.md)。 在“线程”窗口中，可以选择显示所有线程或仅显示标记的线程  。

### <a name="to-display-only-flagged-threads"></a>仅显示标记的线程

- 选择**仅显示标记的线程**顶部的工具栏中**线程**窗口。 （如果灰显，您需要首先标记某些线程。）

## <a name="freeze-and-thaw-threads"></a>冻结和解冻线程
 当冻结线程时，系统不会启动线程的执行，即使提供了资源。

 在本机代码中，您可以挂起或继续线程通过调用 Windows 函数`SuspendThread`和`ResumeThread`。 或者，致电 MFC 函数[CWinThread::SuspendThread](/cpp/mfc/reference/CWinThread-class#suspendthread)并[cwinthread:: Resumethread](/cpp/mfc/reference/CWinThread-class#resumethread)。 如果您调用`SuspendThread`或`ResumeThread`，则*挂起项计数*中所示**线程**窗口将会更改。 如果冻结或解冻本机线程不会更改挂起项计数。 线程不能在本机代码中执行，除非它线程解冻并且其挂起项计数为零。

 在托管代码中，当冻结或解冻线程时，将更改挂起项计数。 如果在托管代码中冻结线程，其挂起项计数为 1。 当本机代码中冻结线程时，其挂起项计数为 0，除非使用`SuspendThread`调用。

> [!NOTE]
> 在调试本机代码对托管代码的调用时，托管代码与调用它的本机代码在同一个物理线程中运行。 挂起或冻结本机线程也会冻结托管代码。

### <a name="to-freeze-or-thaw-execution-of-a-thread"></a>冻结或解冻线程的执行

- 在顶部的工具栏**线程**窗口中，选择**冻结线程**或**解冻线程**。

     此操作仅影响在“线程”窗口中选中的线程  。

### <a name="switch-to-another-thread"></a>切换到另一个线程

黄色箭头指示当前线程 （和执行指针的位置）。 带有卷尾的绿色箭头指示非当前线程具有当前的调试器上下文。

#### <a name="to-switch-to-another-thread"></a>若要切换到另一个线程

- 请按照以下步骤之一操作：

  - 双击任一线程。

  - 右击一个线程，然后选择**切换到线程**。

## <a name="group-and-sort-threads"></a>分组和排序线程
 分组线程时，表中将显示每组的标题。 标题包含组说明（如“辅助线程”或“未标记的线程”）和树控件   。 每组的成员线程显示在组标题下。 如果你想要隐藏组的成员线程，使用树控件折叠组。

 因为分组优先于排序，所以您可以先按类别（以此为例）分组线程，再按每个类别中的 ID 对其进行排序。

### <a name="to-sort-threads"></a>排序线程

1. 在顶部的工具栏**线程**窗口中，选择任意列顶部的按钮。

     线程现在按该列中的值进行排序。

2. 如果你想要反转排序顺序，请再次选择相同的按钮。

     在列表顶部显示的线程现在显示在底部。

### <a name="to-group-threads"></a>分组线程

- 在中**线程**窗口工具栏中，选择**分组依据**列表，然后选择要分组线程所依据的条件。

### <a name="to-sort-threads-within-groups"></a>对组内线程排序

1. 在顶部的工具栏**线程**窗口中，选择**分组依据**列表，然后选择要分组线程所依据的条件。

2. 在中**线程**窗口中，选择任意列顶部的按钮。

     线程现在按该列中的值进行排序。

### <a name="to-expand-or-collapse-all-groups"></a>展开或折叠所有组

- 在顶部的工具栏**线程**窗口中，选择**展开组**或**折叠组**。

## <a name="search-for-specific-threads"></a>搜索特定的线程
 您可以搜索匹配的指定的字符串中的线程**线程**窗口。 在搜索线程时，窗口将显示匹配的任何列中的搜索字符串的所有线程。 信息包括在“位置”列中调用堆栈顶部显示的线程位置  。 默认情况下，不搜索整个调用堆栈。

### <a name="to-search-for-specific-threads"></a>搜索特定线程

1. 在“线程”窗口顶部的工具栏中，转到“搜索”框，执行下列操作之一   ：

     - 输入搜索字符串，然后按**Enter**。

     \- 或 -

     - 选择下拉列表旁边**搜索**框并选择上一次搜索的搜索字符串。

2. （可选）若要在搜索中包括整个调用堆栈，请选择“搜索调用堆栈”  。

## <a name="display-thread-call-stacks-and-switch-between-frames"></a>显示线程调用堆栈和帧之间切换
在多线程程序中，每个线程都有自己的调用堆栈。 “线程”窗口提供了一种查看这些堆栈的简便方法  。

> [!TIP]
> 对于每个线程的调用堆栈的可视表示形式，使用[并行堆栈](../debugger/get-started-debugging-multithreaded-apps.md)窗口。

### <a name="to-view-the-call-stack-of-a-thread"></a>查看线程的调用堆栈

- 在中**位置**列中，选择线程位置旁边的倒的三角形。

     此位置将展开以显示线程的调用堆栈。

### <a name="to-view-or-collapse-the-call-stacks-of-all-threads"></a>查看或折叠所有线程的调用堆栈

- 在顶部的工具栏**线程**窗口中，选择**展开调用堆栈**或**折叠调用堆栈**。

## <a name="see-also"></a>请参阅
- [调试多线程应用](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [开始调试多线程应用程序](../debugger/get-started-debugging-multithreaded-apps.md)
