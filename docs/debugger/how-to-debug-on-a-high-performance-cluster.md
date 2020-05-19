---
title: 如何：在高性能群集上进行调试 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- cluster debugging
- high-performance debugging
ms.assetid: a2f0eb07-840e-4f95-a1b1-9509217e5b8f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d95c6eeadfdf1bb90471997712299ae03a945be8
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72733669"
---
# <a name="how-to-debug-on-a-high-performance-cluster-c-visual-basic-c"></a>如何：在高性能群集上进行调试（C#、Visual Basic、C++）

在高性能群集上调试多处理程序类似于在远程计算机上调试普通程序。 但是，还有一些其他注意事项。 有关常规的远程设置要求，请参阅[远程调试](../debugger/remote-debugging.md)。

 当在高性能群集上进行调试时，可以使用所有可用于远程调试的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 调试窗口和技术。 但是由于你正在进行远程调试，所以外部控制台窗口不可用。

 “线程”窗口和“进程”窗口对于调试并行应用程序特别有用 。 有关如何使用这些窗口的提示，请参阅[如何：使用“进程”窗口](/previous-versions/visualstudio/visual-studio-2010/7h8h5sdw(v=vs.100))和[演练：使用“线程”窗口进行调试](../debugger/how-to-use-the-threads-window.md)。

 下面的过程演示在高性能群集上调试时特别有用的一些技术。

 调试并行应用程序时，你可能希望在特定的线程、进程或计算机上设置断点。 可以通过创建普通断点，然后添加断点筛选器来做到这一点。

### <a name="to-open-the-breakpoint-filter-dialog-box"></a>打开“断点筛选器”对话框

1. 在源窗口、“反汇编”窗口、“调用堆栈”窗口或“断点”窗口中右键单击断点标志符号  。

2. 在快捷菜单上，单击“筛选器”。 此选项可能显示在顶级菜单上或者显示在“断点”之下的子菜单中。

### <a name="to-set-a-breakpoint-on-a-specific-computer"></a>在特定计算机中设置断点

1. 从“进程”窗口中获取计算机名。

2. 选择一个断点，并如上一过程中所描述的那样打开“断点筛选器”对话框。

3. 在“断点筛选器”对话框中键入以下内容：

     MachineName =你的计算机名

     若要创建更复杂的筛选器，可以使用 `&`（“与”运算符）、`||`（“或”运算符）、`!`（“非”运算符）和括号组合子句。

4. 单击 **“确定”** 。

### <a name="to-set-a-breakpoint-on-a-specific-process"></a>在特定进程上设置断点

1. 从“进程”窗口获取进程名称或进程 ID 号。

2. 选择一个断点，并如第一个过程中所描述的那样打开“断点筛选器”对话框。

3. 在“断点筛选器”对话框中键入以下内容：

     `ProcessName =` 你的进程名

     \- 或 -

     `ProcessID =` 你的进程 ID 号

     若要创建更复杂的筛选器，可以使用 `&`（“与”运算符）、`||`（“或”运算符）、`!`（“非”运算符）和括号组合子句。

4. 单击 **“确定”** 。

### <a name="to-set-a-breakpoint-on-a-specific-thread"></a>在特定线程上设置断点

1. 从“线程”窗口中获取线程名称或线程 ID 号。

2. 选择一个断点，并如第一个过程中所描述的那样打开“断点筛选器”对话框。

3. 在“断点筛选器”对话框中键入以下内容：

     `ThreadName =` 你的线程名称

     \- 或 -

     `ThreadID =` 你的线程 ID 号

     若要创建更复杂的筛选器，可以使用 `&`（“与”运算符）、`||`（“或”运算符）、`!`（“非”运算符）和括号组合子句。

4. 单击 **“确定”** 。

## <a name="example"></a>示例
 下面的示例演示如何在名为 `marvin` 的计算机上的、名为 `fourier1` 的线程上创建一个断点筛选器。

`(MachineName = marvin) & (ThreadName = fourier1)`

## <a name="see-also"></a>请参阅
- [调试多线程应用程序](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [远程调试](../debugger/remote-debugging.md)
- [如何：使用“进程”窗口](/previous-versions/visualstudio/visual-studio-2010/7h8h5sdw(v=vs.100))
- [开始调试多线程应用](../debugger/get-started-debugging-multithreaded-apps.md)
- [线程和进程](/previous-versions/visualstudio/visual-studio-2010/ms164740(v=vs.100))
- [使用断点](../debugger/using-breakpoints.md)