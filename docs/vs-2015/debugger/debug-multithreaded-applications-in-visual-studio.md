---
title: 调试多线程应用程序
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.gputthreads
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- threading [Visual Studio], debugging
- debugging [Visual Studio], high-performance computing
- debugging [Visual Studio], multithreaded
- multithreaded debugging
- high-performance debugging
ms.assetid: 9d175bc2-1d95-4c47-9bc3-9755af968a9c
caps.latest.revision: 28
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8cb43c9a32f3dfd0a6383d466f7cd283acf0ab3a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65691283"
---
# <a name="debug-multithreaded-applications-in-visual-studio"></a>在 Visual Studio 中调试多线程应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

线程是操作系统向其分配处理器时间的指令序列。 在操作系统中运行的每个进程都包含至少一个线程。 包含多个线程的进程称为多线程。

 具有多个处理器、多核处理器或超线程进程的计算机可以同时运行多个线程。 并行处理多个线程可以极大地提高程序性能，但是，由于需要跟踪多个线程，也使得调试更加困难。

 此外，多线程处理会引入某些新类型的潜在 bug。 例如，通常会有两个或更多线程必须访问同一资源，但是一次只能有一个线程可以安全地访问该资源。 必须使用某种形式的互斥以确保一次仅有一个线程访问资源。 如果互斥执行不正确，则可以创建不能执行任何线程的 *死锁* 情况。 对于调试而言，死锁是特别难解决的问题。

 Visual Studio 提供了 " **线程** " 窗口、"GPU 线程" 窗口、"并行" 监视窗口以及使多线程调试更容易的其他功能。 了解线程界面功能的最佳方法是执行演练。 请参阅 [演练：调试多线程应用程序](../debugger/walkthrough-debugging-a-multithreaded-application.md) 和 [演练：调试 C++ AMP 应用程序](https://msdn.microsoft.com/library/40e92ecc-f6ba-411c-960c-b3047b854fb5)。

 Visual Studio 还提供了功能强大的断点和跟踪点，在调试多线程应用程序时，它们十分有用。 可以使用断点筛选器将断点置于单个线程上。 请参阅 [使用断点](../debugger/using-breakpoints.md)

 调试具有用户界面的多线程应用程序可能会特别困难。 在这种情况下，可以考虑在另一台机器上运行应用程序并使用远程调试。 有关信息，请参阅 [远程调试](../debugger/remote-debugging.md)。

## <a name="in-this-section"></a>本节内容
 [调试线程和进程](../debugger/debug-threads-and-processes.md) 介绍调试线程和进程的基本知识。

 [调试多个进程](../debugger/debug-multiple-processes.md) 说明如何调试多个进程。

 [如何：使用 "线程" 窗口](../debugger/how-to-use-the-threads-window.md) 通过 " **线程** " 窗口调试线程的实用过程。

 [如何：在调试时切换到另一个线程](../debugger/how-to-switch-to-another-thread-while-debugging.md) 将调试上下文切换到其他线程的三种方法。

 [如何：标记线程和取消标记线程](../debugger/how-to-flag-and-unflag-threads.md) 在调试时标记或标记要特别注意的线程。

 [如何：在本机代码中设置线程名称](../debugger/how-to-set-a-thread-name-in-native-code.md) 为线程指定一个在 " **线程** " 窗口中查看的名称。

 [如何：在托管代码中设置线程名称](../debugger/how-to-set-a-thread-name-in-managed-code.md) 为线程指定一个在 " **线程** " 窗口中查看的名称。

 [演练：调试多线程应用程序](../debugger/walkthrough-debugging-a-multithreaded-application.md)。
一部关于线程调试功能的指导教程，重点介绍如何使用 [!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)] 的功能。

 [如何：在高性能群集上进行调试](../debugger/how-to-debug-on-a-high-performance-cluster.md) 用于调试在高性能群集上运行的应用程序的技术。

 [调试本机代码中的线程时的提示](../debugger/tips-for-debugging-threads-in-native-code.md) 可用于调试本机线程的简单技术。

 [使用 "任务" 窗口](../debugger/using-the-tasks-window.md) 显示所有托管或本机任务对象（包括其状态和其他有用信息）的列表。

 [使用 "并行堆栈" 窗口](../debugger/using-the-parallel-stacks-window.md) 在单个视图中显示多个线程 (或任务) 的调用堆栈，并且还会合并 (或任务) 的线程之间通用的堆栈段。

 [演练：调试并行应用程序](../debugger/walkthrough-debugging-a-parallel-application.md) 演示如何使用 "并行任务" 和 "并行堆栈" 窗口的演练。

 [如何：使用 "并行监视" 窗口](../debugger/how-to-use-the-parallel-watch-window.md) 跨多个线程检查值和表达式。

 [如何：使用 "GPU 线程" 窗口](../debugger/how-to-use-the-gpu-threads-window.md) 检查并使用调试过程中在 GPU 上运行的线程。

## <a name="related-sections"></a>相关章节

[使用断点](../debugger/using-breakpoints.md)
- 如果要将一个断点置于单个线程上，可以使用断点筛选器。

- 使用跟踪点可以在不中断的情况下跟踪程序的执行。 对于研究死锁之类的问题，这一点十分有用。

  [线程处理](https://msdn.microsoft.com/library/7b46a7d9-c6f1-46d1-a947-ae97471bba87) 编程中的线程处理概念 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ，包括代码示例。

  [组件中的多线程处理](https://msdn.microsoft.com/library/2fc31e68-fb71-4544-b654-0ce720478779) 如何在组件中使用多线程处理 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。

  [针对旧代码的多线程支持 (Visual C++) ](https://msdn.microsoft.com/library/24425b1f-5031-4c6b-aac7-017115a40e7c) 使用 MFC 的 c + + 程序员的线程处理概念和代码示例。

## <a name="see-also"></a>另请参阅
 [调试线程和进程](../debugger/debug-threads-and-processes.md)[远程调试](../debugger/remote-debugging.md)
