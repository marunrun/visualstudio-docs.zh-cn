---
title: DA0039：锁争用率非常高 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.39
- vs.performance.DA0039
- vs.performance.rules.DA0039
ms.assetid: 5a9fc57d-9097-413b-af0c-8726b1a57048
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f441cb5e6f8febf374a9ea024db9bec95960e11b
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444857"
---
# <a name="da0039-very-high-rate-of-lock-contentions"></a>DA0039：锁争用率非常高

|||
|-|-|
|规则 ID|DA0039|
|类别|.NET Framework 使用情况|
|分析方法|采样<br /><br /> 检测<br /><br /> .NET 内存|
|消息|.NET 锁争用率非常高。 请运行“并发”分析调查出现此锁争用的原因。|
|规则类型|警告|

 使用采样法、.NET 内存或资源争用方法进行分析时，必须至少收集 25 个样本才能触发此规则。

## <a name="cause"></a>原因
 与分析数据一起收集的系统性能数据表示：应用程序执行期间的锁争用率过高。 请再次考虑使用并发分析进行分析，以找出争用的起因。

## <a name="rule-description"></a>规则说明
 锁用于保护代码的关键部分，这些关键部分必须由一个线程在多线程应用程序上一次按顺序执行。 Microsoft .NET 公共语言运行时 (CLR) 提供了一套完整的同步和锁定基元。 例如，C# 语言支持 lock 语句（Visual Basic 中的 SyncLock）。 托管应用程序可调用 System.Threading 命名空间中的 Monitor.Enter 和 Monitor.Exit 方法，从而直接获取和释放 lock。 .NET Framework 支持其他同步和锁定基元，包括支持互斥锁、ReaderWriterLock 和信号量的类。 有关详细信息，请参阅 MSDN 网站上“.NET Framework 开发人员指南”中的 [Overview of Synchronization Primitives](http://go.microsoft.com/fwlink/?LinkId=177867)（同步基元概述）。 .NET Framework 类本身分层在 Windows 操作系统内置的级别较低的同步服务上。 其中包括关键部分对象和很多不同的 Wait 和事件信号函数。 有关详细信息，请参阅 MSDN 库中“Win32 和 COM 开发”的 [Synchronization](http://go.microsoft.com/fwlink/?LinkId=177869)（同步）部分。

 用于同步和锁定的 .NET Framework 类和 Windows 对象以共享内存位置为基础，且必须使用互锁操作才能更改该共享内存位置。 通过在共享内存位置进行操作的特定于硬件的说明，互锁操作使用原子操作更改其状态。 应确保原子操作在计算机的所有处理器中保持一致。 lock 和 WaitHandles 是 .NET 对象，设置或重置二者时，它们将自动使用互锁操作。 应用程序中可能有其他共享内存数据结构，需使用互锁操作才能以线程安全的方式进行更新。 有关详细信息，请参阅 MSDN 库 .NET Framework 部分中的[互锁操作](http://go.microsoft.com/fwlink/?LinkId=177870)。

 同步和锁定是确保正确执行多线程应用程序的机制。 多线程应用程序的每个线程都是由操作系统单独安排的独立执行单元。 每当尝试获取锁的线程因另一线程持有锁而延迟时，都将出现锁争用。

 锁经常嵌套。 执行关键部分的线程执行需要另一锁的函数时，会出现嵌套。 一定量的锁嵌套是无法避免的。 关键部分可调用依赖于锁的 .NET Framework 方法，以确保其线程安全。 应用程序中某些关键部分调用使用其他锁句柄进行锁定的 Framework 方法时会导致锁嵌套。 嵌套的锁定条件可导致难以解决和修复的性能问题。

 分析运行期间采用的测量值表明锁争用过高时，将触发此规则。 锁争用将延迟执行等待锁的线程。 即使是在低端硬件上运行的单元测试或负载测试中的少量锁争用，也应进行调查。

> [!NOTE]
> 分析数据中报告的锁争用率非常高但没有过量时，将触发 [DA0038：锁争用率高](../profiling/da0038-high-rate-of-lock-contentions.md)信息消息，不会触发此警告消息。

## <a name="how-to-investigate-a-warning"></a>如何调查警告
 双击消息导航到分析数据的[“标记”](../profiling/marks-view.md)视图。  查找 **.NET CLR LocksAndThreads\Contention Rate / sec** 列。 确定是否存在特定阶段的程序执行，其中锁争用高于其他阶段。

 仅在未使用并发分析方法时才会触发此规则。 并发分析方法是诊断应用程序中与锁争用相关的性能问题的最好工具。 收集并发分析数据，以便了解应用程序的锁定行为。 包括了解哪些锁争用较严重、等待争用锁时延迟的线程执行时间，以及其中涉及哪些特定代码。 并发分析收集所有锁争用的数据，包括本机 Windows 设备、.NET Framework 类和应用程序引用的任何其他第三方库的锁定行为。 有关 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE 中的并发分析的详细信息，请参阅[收集线程和进程并发数据](../profiling/collecting-thread-and-process-concurrency-data.md)。 有关命令行中的并发分析的信息的链接，请参阅[使用命令行中的分析方法](../profiling/using-profiling-methods-to-collect-performance-data-from-the-command-line.md)的“使用并发方法收集资源争用和线程活动数据”部分。