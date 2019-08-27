---
title: .NET Framework 使用性能规则 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ab573755-6370-48aa-853d-a7321c424c79
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6bf47871b8b1c2e6f8e4f67bf26ba5f73ca078c7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62970013"
---
# <a name="net-framework-usage-performance-rules"></a>.NET Framework 使用情况性能规则
.Net Framework 使用类别中的性能规则标识可以优化的特定方法，并且还标识可调查性能问题的更为通用的使用模式，例如垃圾回收和锁争用。

|||
|-|-|
|[DA0001：将 StringBuilder 用于串联](../profiling/da0001-use-stringbuilder-for-concatenations.md)|对 <xref:System.String.Concat(System.String,System.String)?displayProperty=fullName> 的调用在分析数据中占很大比例。 请考虑使用 <xref:System.Text.StringBuilder> 类从多个段构造字符串。|
|[DA0005：频繁执行 GC2 收集](../profiling/da0005-frequent-gc2-collections.md)|第 2 代垃圾回收期间回收相对大量的 .NET 内存对象。 如果过多生存期较短的对象在第 1 代回收后仍然存在，那么内存管理的成本将很容易变得过高。|
|[DA0006：为值类型重写 Equals()](../profiling/da0006-override-equals-parens-for-value-types.md)|对 `Equals` 方法的调用或公共值类型的相等运算符是分析数据的重要组成部分。 请考虑实施更有效的方法。|
|[DA0007：避免对控制流使用异常](../profiling/da0007-avoid-using-exceptions-for-control-flow.md)|分析数据中调用了速率较高的 .NET Framework 异常处理程序。 请考虑使用其他控制流逻辑，以便减少引发的异常数。|
|[DA0010：高开销 GetHashCode](../profiling/da0010-expensive-gethashcode.md)|对类型的 `GetHashCode` 方法的调用是分析数据的重要组成部分，或是 `GetHashCode` 方法分配内存。 降低方法的复杂性。|
|[DA0011：高开销 CompareTo](../profiling/da0011-expensive-compareto.md)|类型的 `CompareTo` 方法开销较大或方法分配内存。 降低 `CompareTo` 方法的复杂性。|
|[DA0012：大量反射](../profiling/da0012-significant-amount-of-reflection.md)|对 <xref:System.Reflection?displayProperty=fullName> 方法（例如 <xref:System.Reflection.IReflect.InvokeMember%2A> 和 <xref:System.Reflection.IReflect.GetMember%2A>）或 Type 方法（例如 <xref:System.Type.InvokeMember%2A>）的调用在分析数据中占很大比例。 如果可能，请考虑用对依赖程序集方法的早期绑定来替代这些方法。|
|[DA0013：String.Split 或 String.Substring 的使用率高](../profiling/da0013-high-usage-of-string-split-or-string-substring.md)|对 <xref:System.String.Split%2A?displayProperty=fullName> 或 <xref:System.String.Substring%2A> 方法的调用在分析数据中占很大比例。 如果要测试字符串中的子字符串是否存在，请考虑使用 <xref:System.String.IndexOf%2A> 或 <xref:System.String.IndexOfAny%2A>。|
|[DA0018：运行的 32 位应用程序达到了进程托管内存限制](../profiling/da0018-32-bit-application-running-at-process-managed-memory-limits.md)|在分析运行期间收集的系统数据表明：.NET Framework 内存堆接近在 32 位进程中可以达到的托管堆的最大大小。 请考虑使用 .NET 内存分析方法再次进行分析，并优化应用程序对托管资源的使用。|
|[DA0021：第 1 代垃圾回收率高](../profiling/da0021-high-rate-of-gen-1-garbage-collections.md)|第 1 代垃圾回收期间回收相对大量的 .NET 内存对象。 如果过多生存期较短的对象在第 0 代回收后仍然存在，那么内存管理的成本将很容易变得过高。|
|[DA0022：第 2 代垃圾回收率高](../profiling/da0022-high-rate-of-gen-2-garbage-collections.md)|第 2 代垃圾回收期间回收大量的 .NET 内存对象。 如果过多生存期较短的对象在第 1 代回收后仍然存在，那么内存管理的成本将很容易变得过高。 锁争用率超过 DA0005 规则的阈值上限值时将触发此规则。|
|[DA0023：GC 占用的 CPU 时间多](../profiling/da0023-high-gc-cpu-time.md)|分析期间收集的系统性能数据表明：垃圾回收所用的时间明显超过应用程序总处理时间。|
|[DA0024：GC 占用的 CPU 时间过多](../profiling/da0024-excessive-gc-cpu-time.md)|分析期间收集的系统性能数据表明：垃圾回收所用的时间明显超过应用程序总处理时间。 垃圾回收中花费的时间超过 DA0023 规则的阈值上限值时，将触发此规则。|
|[DA0038：锁争用率高](../profiling/da0038-high-rate-of-lock-contentions.md)|与分析数据一起收集的系统性能数据表示：应用程序执行期间的锁争用率非常高。 请再次考虑使用并发分析进行分析，以找出争用的起因。|
|[DA0039：锁争用率非常高](../profiling/da0039-very-high-rate-of-lock-contentions.md)|与分析数据一起收集的系统性能数据表示：应用程序执行期间的锁争用率过高。 请再次考虑使用并发分析进行分析，以找出争用的起因。 锁争用率高于 DA0038 规则的阈值上限值时将触发此规则。|