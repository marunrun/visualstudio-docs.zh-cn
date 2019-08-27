---
title: 性能不佳的多线程应用程序的常见模式 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.tools.gallery
helpviewer_keywords:
- Concurrency Visualizer, common patterns for poorly-behaved multithreaded applications
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4aec033266ccb2a6e6dcd0342669b7c31082488a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62788852"
---
# <a name="common-patterns-for-poorly-behaved-multithreaded-applications"></a>性能不佳的多线程应用程序的常见模式

并发可视化工具可帮助开发者将多线程应用程序的行为可视化。 此工具包含性能不佳的多线程应用程序的常见模式库。 该库包括通过工具公开的典型、可识别的视觉对象模式，以及每种模式所表示的行为的解释，该行为可能造成的结果以及解决它最常用的方法。

## <a name="lock-contention-and-serialized-execution"></a>锁争用和序列化执行

![锁争用导致序列化执行](../profiling/media/lockcontention_serialized.png "LockContention_Serialized")

有时，即使并行化应用程序有多个线程，并且计算机有足够数量的逻辑内核，它仍会顽固地继续串行执行。 第一个症状是较差的多线程性能，甚至可能比串行实现要稍慢。 在“线程”视图中，看不到并行运行的多个线程；相反，将看到在任何时候都只有一个线程运行。 在这种情况下，如果单击线程中的同步段，则可以看到被阻塞线程的调用堆栈（阻塞调用堆栈）和删除阻塞条件的线程（取消阻塞调用堆栈）。 此外，如果正在分析的进程中发生取消阻塞调用堆栈，将显示线程就绪连接符。 从这点上看，可以在阻塞和取消阻塞调用堆栈中导航到代码，以进一步调查造成序列化的原因。

如下图所示，并发可视化工具还可在 CPU 使用率视图中公开此症状，其中，尽管存在多个线程，但该应用程序只使用一个逻辑核心。

有关详细信息，请参阅 MSDN 杂志文章[线程性能 - Visual Studio 2010 中的资源争用并发分析](https://msdn.microsoft.com/magazine/ff714587.aspx)中的“从问题开始”部分。

![锁争用](../profiling/media/lockcontention_2.png "LockContention_2")

## <a name="uneven-workload-distribution"></a>不均匀的工作负载分布

![不均匀的工作负载](../profiling/media/unevenworkload_1.png "UnevenWorkLoad_1")

如上图所示，应用程序中多个并行线程之间的工作分布不规则时，在每个线程完成其工作时会出现典型的阶梯状模式。 并发可视化工具最常为每个并发线程显示非常接近的启动时间。 但是，这些线程通常以不规则的方式结束，而不是同时结束。 这种模式表示一组并行线程间不规则的工作分配，这可能导致性能下降。 解决此类问题的最佳方式是重新评估在并行线程中划分工作的算法。

如下图所示，并发可视化工具在 CPU 使用率视图中以 CPU 使用率逐步下降的方式公开此症状。

![不均匀的工作负载](../profiling/media/unevenworkload_2.png "UnevenWorkload_2")

## <a name="oversubscription"></a>过度订阅

![过度订阅](../profiling/media/oversubscription.png "Oversubscription")

在出现过度订阅的情况下，进程中活动线程的数量将超出系统上可用的逻辑内核数。 上图显示过度订阅的结果，以及所有活动线程中明显的抢占区段。 此外，图例显示了抢占占用了大部分的时间（在本例中为 84%）。 这可能表示进程正在要求系统执行多于逻辑核心数的并发线程。 但是，这也可能表示系统上的其他进程正在使用假设为此进程所提供的资源。

评估此问题时，应注意以下事项：

- 整个系统可能被过度订阅。 请考虑到系统上的其他进程可能会抢占线程。 将光标悬停在“线程”视图中的抢占段时，工具提示将识别该线程和抢占该线程的进程。 此进程不一定是在进程被抢占的整个过程中执行的进程，但它可提供是什么对进程造成了抢占压力的相关提示。

- 评估进程如何确定在此工作阶段期间要执行的线程的合适数量。 如果进程直接计算活动的并行线程数，请考虑修改算法以更好地在系统上占用可用的逻辑内核数。 如果使用并发运行时、任务并行库或 PLINQ，这些库将执行计算线程数的工作。

## <a name="inefficient-io"></a>I/O 效率低

![I/O 效率低](../profiling/media/inefficient_io.png "Inefficient_IO")

过度使用或误用 I/O 是导致应用程序效率低下的常见原因。 请参考上图。 可见时间线分析显示 I/O 使用了 44% 的可见线程时间。 时间线显示大量 I/O，这指示 I/O 频繁地阻塞被分析应用程序。 若要深入了解 I/O 类型和程序被阻塞的位置，请放大存在问题的区域，检查可见时间线分析，然后单击特定 I/O 块以查看当前的调用堆栈。

## <a name="lock-convoys"></a>锁保护

![锁保护](../profiling/media/lock_convoys.png "Lock_Convoys")

当应用程序要求以先到先得的顺序锁定和锁定处的到达率高于获取率时将发生锁保护。 这两个条件的组合会导致要求锁开始进行备份。 解决此问题的一种方法是使用“不公平”锁或使用授予第一个线程访问权限的锁，以在未锁定状态中找到查找它们。 上图显示了此保护行为。 若要解决此问题，请尝试减少同步对象的争用并尝试使用不公平锁。

## <a name="see-also"></a>请参阅

[线程视图](../profiling/threads-view-parallel-performance.md)