---
title: 按 ID 列出的性能规则 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 9a1c934c-4798-4df9-a8ef-eb17ef06b6a2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3878f22e37c281235e62e025c6b73779d3478f8b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62798362"
---
# <a name="performance-rules-by-id"></a>按 ID 排序的性能规则

| 警告 | 说明 |
| - | - |
| [DA0001：将 StringBuilder 用于串联](../profiling/da0001-use-stringbuilder-for-concatenations.md) | 对 System.String.Concat 的调用是分析数据的重要组成部分。 请考虑使用 <xref:System.Text.StringBuilder> 类从多个段构造字符串。 |
| [DA0002：缺少 VSPerfCorProf.dll](../profiling/da0002-vsperfcorprof-dll-is-missing.md) | 探查器在分析运行期间找不到 VSPerfCorProf.dll。 当使用命令行工具收集探查器数据，但未使用 VSPerfCLREnv.cmd 工具初始化必要的环境变量时，将出现此警告。 |
| [DA0003：大量内核样本](../profiling/da0003-many-kernel-samples.md) | 为应用程序收集的很大一部分调用堆栈样本在内核模式下执行。 请考虑使用其他分析方法分析应用程序。 |
| [DA0004：处理器使用率高](../profiling/da0004-high-processor-usage.md) | 使用检测方法分析收集的数据时，处理器 (CPU) 使用率很高。 分析 CPU 密集型应用程序时，请考虑使用采样分析方法。 |
| [DA0005：频繁执行 GC2 收集](../profiling/da0005-frequent-gc2-collections.md) | 第 2 代垃圾回收期间回收大量的 .NET 内存对象。 |
| [DA0006：为值类型重写 Equals()](../profiling/da0006-override-equals-parens-for-value-types.md) | 对 Equals 方法或公共值类型的相等运算符的调用在分析数据中占很大比例。 请考虑实施更有效的方法。 |
| [DA0007：避免对控制流使用异常](../profiling/da0007-avoid-using-exceptions-for-control-flow.md) | 分析数据中调用了速率较高的 .NET Framework 异常处理程序。 请考虑使用其他控制流逻辑，以便减少引发的异常数。 |
| [DA0008：已收集的样本极少](../profiling/da0008-few-samples-collected.md) | 分析运行期间仅收集了少量样本。 请考虑运行更长的时间或使用更快的采样率，以获取更有意义的结果。 |
| [DA0009：JIT 所占时间百分比很高](https://msdn.microsoft.com/b60c1767-515c-41d9-81c2-c70d0b7024fd) | 实时 (JIT) 编译器所用的时间占应用程序执行时间的百分比很大。 |
| [DA0010：高开销 GetHashCode](../profiling/da0010-expensive-gethashcode.md) | 对该类型的 GetHashCode 方法的调用在分析数据中占很大比例或此方法分配内存。 |
| [DA0011：高开销 CompareTo](../profiling/da0011-expensive-compareto.md) | 类型的 CompareTo 方法开销巨大或分配内存。 |
| [DA0012：大量反射](../profiling/da0012-significant-amount-of-reflection.md) | 对 System.Reflection 方法（如 InvokeMember 和 GetMember）或 Type 方法（如 MemberInvoke）的调用是分析数据的重要组成部分。 如果可以，请考虑用对依赖程序集的方法的早期绑定替代这些方法。 |
| [DA0013：String.Split 或 String.Substring 的使用率高](../profiling/da0013-high-usage-of-string-split-or-string-substring.md) | 对 System.String.Split 或 System.String.Substring 方法的调用在分析数据中占很大比例。 如果测试字符串中是否存在子字符串，请考虑使用 System.String.IndexOf 或 System.String.IndexOfAny。 |
| [DA0014：以分页方式将活动内存移到磁盘的发生率极高](../profiling/da0014-extremely-high-rates-of-paging-active-memory-to-disk.md) | 在分析运行中收集的系统性能数据表明：在整个分析运行期间，活动内存到磁盘的分页速率或从磁盘中分页活动内存的速率很高。 此级别的分页速率通常会影响应用程序性能和响应能力。 请考虑通过修改算法来减少内存分配。 还可能需考虑应用程序的内存要求或在拥有更多内存的计算机上重新运行分析。 |
| [DA0017：以分页方式将活动内存移到磁盘的发生率高](../profiling/da0017-high-rates-of-paging-active-memory-to-disk.md) | 在分析运行中收集的系统性能数据表明：在整个分析运行期间，活动内存到磁盘的分页速率或从磁盘中分页活动内存的速率较高。 此级别的分页速率通常会影响应用程序性能和响应能力。 请考虑通过修改算法来减少内存分配。 还可能需考虑应用程序的内存要求或在拥有更多内存的计算机上重新运行分析。 |
| [DA0018：运行的 32 位应用程序达到了进程托管内存限制](../profiling/da0018-32-bit-application-running-at-process-managed-memory-limits.md) | 分析运行期间收集的系统数据表明：.NET Framework 内存堆已接近托管堆在 32 位进程中可以达到的最大大小。 报告的值是被分析进程处于活动状态时堆的最大观测值。 请考虑优化应用程序对托管资源的使用。 |
| [DA0021：第 1 代垃圾回收率高](../profiling/da0021-high-rate-of-gen-1-garbage-collections.md) | 分析期间收集的系统性能数据表明：与第 0 代数据收集相比，第 1 代垃圾回收中为 .NET Framework 对象回收的内存比例较高。 |
| [DA0022：第 2 代垃圾回收率高](../profiling/da0022-high-rate-of-gen-2-garbage-collections.md) | 分析期间收集的系统性能数据表明：与第 0 代和第 1 代垃圾回收相比，第 2 代垃圾回收中为 .NET Framework 对象回收的内存比例较高。 |
| [DA0023：GC 占用的 CPU 时间多](../profiling/da0023-high-gc-cpu-time.md) | 分析期间收集的系统性能数据表明：与应用程序总处理时间相比，垃圾回收所用时间较长。 |
| [DA0024：GC 占用的 CPU 时间过多](../profiling/da0024-excessive-gc-cpu-time.md) | 分析期间收集的系统性能数据表明：与应用程序总处理时间相比，垃圾回收所用时间过长。 |
| [DA0026：过多内核 CPU 时间处理](../profiling/da0026-excessive-kernel-cpu-time-processing.md) | 内核模式下执行的 CPU 时间比例超过在用户模式下所花费的时间。 请考虑重新进行分析并对系统调用 (syscalls) 的数量进行采样，确定内核模式执行次数较多的原因。 |
| [DA0029：CLR 版本不受支持](../profiling/da0029-unsupported-clr-version.md) | 你尝试分析的应用程序使用不受分析工具支持的 .NET Framework 1.1 版。 |
| [DA0030：收集数据库项目的“层交互”度量值](../profiling/da0030-gather-tier-interaction-measurements-for-database-projects.md) | 对 <xref:System.Data> 方法的调用在分析数据中占很大比例，并且你未收集分析运行中的层交互数据。 请考虑再次进行分析并添加层交互数据。 |
| [DA0038：锁争用率高](../profiling/da0038-high-rate-of-lock-contentions.md) | 与分析数据一起收集的系统性能数据表明：应用程序执行期间的锁争用率很高。 请再次考虑使用并发分析进行分析，以找出争用的起因。 |
| [DA0039：锁争用率非常高](../profiling/da0039-very-high-rate-of-lock-contentions.md) | 与分析数据一起收集的系统性能数据表明：应用程序执行期间的锁争用率过高。 请再次考虑使用并发分析进行分析，以找出争用的起因。 |
| [DA0501：所分析进程的 CPU 平均消耗量。](../profiling/da0501-average-cpu-consumption-by-the-process-being-profiled.md) | 此消息报告处理器忙于执行应用程序指令的时间的百分比。 报告的值是所分析的进程处于活动状态的所有测量时间间隔的平均值。 具有多个处理器的计算机上的值可能大于 100%。 |
| [DA0502：所分析进程的 CPU 最大消耗量](../profiling/da0502-maximum-cpu-consumption-by-the-process-being-profiled.md) | 此消息报告处理器忙于执行应用程序指令的最高时间百分比。 报告的值是所分析的进程在其中处于活动状态的所有测量间隔中报告的最大值。 具有多个处理器的计算机上的百分比可能大于 100%。 |
| [DA0503：所分析进程的平均工作集（以字节为单位）](../profiling/da0503-average-working-set-in-bytes-for-the-process-being-profiled.md) | 此消息用于报告此进程当前使用的平均物理内存字节数（工作集）。 进程工作集包含当前占用物理内存的进程地址空间中的页面。 |
| [DA0504：所分析进程的最大工作集（以字节为单位）](../profiling/da0504-maximum-working-set-in-bytes-for-the-process-being-profiled.md) | 此消息报告进程当前使用的以字节为单位的最大物理内存量。 进程工作集包含当前占用物理内存的进程地址空间中的页面。 此规则报告分析处于活动状态时进程工作集的最大值。 |
| [DA0505：为所分析进程分配的平均专用字节数](../profiling/da0505-average-private-bytes-allocated-for-the-process-being-profiled.md) | 此消息用于报告进程当前已分配的虚拟内存的平均字节数（专用字节）。 专用字节是由进程分配的虚拟内存位置，只能通过进程内部运行的线程访问此进程。 |
| [DA0506：为所分析进程分配的最大专用字节数](../profiling/da0506-maximum-private-bytes-allocated-for-the-process-being-profiled.md) | 此消息报告进程当前已分配的以字节为单位的最大虚拟内存量（专用字节）。 专用字节是由进程分配的虚拟内存位置，只能通过进程内部运行的线程访问此进程。 |
