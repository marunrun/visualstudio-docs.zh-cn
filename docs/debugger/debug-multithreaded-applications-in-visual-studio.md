---
title: 调试多线程应用程序 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/06/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.gputthreads
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- threading [Visual Studio], debugging
- debugging [Visual Studio], high-performance computing
- debugging [Visual Studio], multithreaded
- multithreaded debugging
- high-performance debugging
ms.assetid: 9d175bc2-1d95-4c47-9bc3-9755af968a9c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b3f2fc8b6acd38393cf9fefb1c5581ab4d1a0712
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62852926"
---
# <a name="debug-multithreaded-applications-in-visual-studio"></a>在 Visual Studio 中调试多线程应用程序
线程是操作系统向其授予处理器时间的指令序列。 在操作系统中运行的每个进程都包含至少一个线程。 包含多个线程的进程称为多线程。

具有多个处理器、 多核处理器或超线程进程的计算机可以运行多个并发线程。 并行处理使用多个线程可以极大地提高程序性能，但它还会使调试更加困难因为跟踪多个线程。

多线程处理可能会引入新类型的潜在 bug。 例如，两个或多个线程可能需要访问同一个资源，但一次只有一个线程可以安全地访问资源。 某种形式的互相排斥，才可确保只有一个线程在任何时候访问资源。 如果未正确实现互相排斥时，它可以创建*死锁*任何线程将执行的条件。 死锁很难解决的问题进行调试。

## <a name="tools-for-debugging-multithreaded-apps"></a>用于调试多线程应用程序的工具

Visual Studio 提供不同的工具用于调试多线程应用程序。

- 对于线程，用于调试线程的主要工具是**线程**窗口中，源窗口中的线程标记**并行堆栈**窗口中，**并行监视**窗口中，并**调试位置**工具栏。 若要了解如何**线程**窗口和**调试位置**工具栏中，请参阅[演练：使用“线程”窗口进行调试](../debugger/how-to-use-the-threads-window.md)。 若要了解如何使用**并行堆栈**并**并行监视**windows，请参阅[开始调试多线程应用程序](../debugger/get-started-debugging-multithreaded-apps.md)。 这两个主题显示如何使用线程标记。

- 使用的代码[任务并行库 (TPL)](/dotnet/standard/parallel-programming/task-parallel-library-tpl)或[并发运行时](/cpp/parallel/concrt/concurrency-runtime/)，用于调试的主要工具是**并行堆栈**窗口中， **并行监视**窗口中，并**任务**窗口中，它还支持 JavaScript。 若要开始，请参阅[演练：调试并行应用程序](../debugger/walkthrough-debugging-a-parallel-application.md)和[演练：调试C++AMP 应用程序](/cpp/parallel/amp/walkthrough-debugging-a-cpp-amp-application)。

- 对于调试 GPU 上的线程，主要工具是“GPU 线程”窗口。 请参阅[如何：使用 GPU 线程窗口](../debugger/how-to-use-the-gpu-threads-window.md)。

- 对于进程，主要工具是“附加到进程”对话框、“进程”窗口和“调试位置”工具栏。

Visual Studio 还提供功能强大的断点和跟踪点，在调试多线程应用程序时，可以很有用。 使用断点条件和筛选器将断点置于单个线程上。 跟踪点，您可以跟踪你的程序的执行，而不会中断，研究问题，例如死锁。 有关详细信息，请参阅[断点操作和跟踪点](../debugger/using-breakpoints.md#BKMK_Print_to_the_Output_window_with_tracepoints)。

调试具有用户界面的多线程应用程序可能会特别困难。 您可以考虑在另一台计算机上运行应用程序并使用远程调试。 有关详细信息，请参阅[远程调试](../debugger/remote-debugging.md)。

## <a name="articles-about-debugging-multithreaded-apps"></a>有关调试多线程应用程序的文章

 [开始调试多线程应用程序](../debugger/get-started-debugging-multithreaded-apps.md)

线程调试功能，强调了中的功能的教程**并行堆栈**窗口和**并行监视**窗口。

 [用于调试线程和进程的工具](../debugger/debug-threads-and-processes.md)

列出了用于调试线程和进程的工具的功能。

 [调试多个进程](../debugger/debug-multiple-processes.md)

说明如何调试多个进程。

 [演练：使用“线程”窗口进行调试](../debugger/how-to-use-the-threads-window.md)。

演示如何使用的演练**线程**窗口和**调试位置**工具栏。

 [演练：调试并行应用程序](../debugger/walkthrough-debugging-a-parallel-application.md)

演示如何使用的演练**并行堆栈**并**任务**windows。

 [如何：在调试时切换到另一个线程](../debugger/how-to-switch-to-another-thread-while-debugging.md)

若要将调试上下文切换到另一个线程的多个方法。

 [如何：标记线程和取消标记线程](../debugger/how-to-flag-and-unflag-threads.md)

在调试过程中，标记要格外关注的线程，或为其设置标志。

 [如何：在高性能群集上进行调试](../debugger/how-to-debug-on-a-high-performance-cluster.md)

对运行于高性能群集上的应用程序进行调试的技术。

 [调试本机代码中的线程时的提示](../debugger/tips-for-debugging-threads-in-native-code.md)

对于调试本机线程十分有用的简单技术。

 [如何：在本机代码中设置线程名称](../debugger/how-to-set-a-thread-name-in-native-code.md)

为在“线程”窗口中查看的线程提供一个名称。

 [如何：在托管代码中设置线程名称](../debugger/how-to-set-a-thread-name-in-managed-code.md)

为在“线程”窗口中查看的线程提供一个名称。

## <a name="see-also"></a>请参阅

- [使用断点](../debugger/using-breakpoints.md)
- [线程处理](/dotnet/standard/threading/index)
- [组件中的多线程处理](https://msdn.microsoft.com/Library/2fc31e68-fb71-4544-b654-0ce720478779)
- [针对旧代码的多线程支持 (Visual C++)](/cpp/parallel/multithreading-support-for-older-code-visual-cpp)
- [调试线程和进程](../debugger/debug-threads-and-processes.md)
- [远程调试](../debugger/remote-debugging.md)