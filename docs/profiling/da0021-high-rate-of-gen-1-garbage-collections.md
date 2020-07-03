---
title: DA0021 - 第 1 代垃圾回收速率高 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.21
- vs.performance.DA0021
- vs.performance.rules.DA0021
ms.assetid: ebf5d9b3-a1ac-4688-8f0f-39a85f4dd15f
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: b22341f1e4944b91f86a16af19494a85a2abd013
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544685"
---
# <a name="da0021-high-rate-of-gen-1-garbage-collections"></a>DA0021：第 1 代垃圾回收率高

|项|“值”|
|-|-|
|规则 ID|DA0021|
|类别|.NET Framework 使用情况|
|分析方法|全部|
|消息|第 1 代垃圾回收率非常高。 按设计来说，如果分配了大部分程序的数据结构且其保留时间较长，那么这通常并不是问题。 但是，如果此行为不在计划内，则表示应用程序可能锁定了对象。 如果不能确定，则可收集 .NET 内存分配数据和对象生存期信息，了解应用程序使用的内存分配模式。|
|规则类型|信息|

 使用采样法、.NET 内存或资源争用方法进行分析时，必须收集至少 10 个样本才能触发此规则。

## <a name="cause"></a>原因
 分析期间收集的系统性能数据表明：与 0 代数据回收相比，1 代垃圾回收中回收 .NET Framework 对象的内存比例较高。

## <a name="rule-description"></a>规则说明
 Microsoft .NET 公共语言运行时 (CLR) 提供自动内存管理机制，该机制使用垃圾回收器从应用程序不再使用的对象回收内存。 垃圾回收器是面向生成的，基于大量分配为短期分配的假设。 例如，局部变量应是短期的。 新创建的对象在 0 代中启动，如果在垃圾回收后它们仍然存在，则将提升到 1 代，如果应用程序仍使用它们，则最后将过渡到 2 代。

 收集 0 代中的对象时，通常频率和效率都较高。 收集 1 代中的对象时，通常频率和效率都较低。 最后，应以更低的频率收集 2 代中生存期较长的对象。 2 代回收是完整的垃圾回收运行，也是成本最高的操作。

 1 代垃圾回收比例过高时将触发此规则。 如果过多生存期较短的对象通过 0 代回收，但在1 代回收中被回收，那么内存管理的成本将过高。 有关详细信息，请参阅 MSDN 网站上 Rico Mariani 关于性能问题的见解的 [Mid-life crisis](https://blogs.msdn.microsoft.com/ricom/2003/12/04/mid-life-crisis/)（中年危机）一文。

## <a name="how-to-investigate-a-warning"></a>如何调查警告
 双击“错误列表”窗口中的消息，导航到分析数据的[标记视图](../profiling/marks-view.md)。 查找 **.NET CLR Memory\\# of Gen 0 Collections** 和 **.NET CLR Memory\\# of Gen 1 Collections** 列。 确定是否存在特定阶段的程序执行，其中垃圾回收更频繁。 将这些值与 **%Time in GC** 列进行比较，查看托管内存分配的模式是否会导致内存管理开销过多。

 若要了解应用程序的托管内存使用模式，请运行 .NET 内存分配分析再次进行分析，并请求“对象生存期”度量值。

 有关如何提高垃圾回收性能的信息，请参阅 Microsoft 网站上的 [Garbage Collector Basics and Performance Hints](/previous-versions/dotnet/articles/ms973837(v=msdn.10))（垃圾回收器基础知识和性能提示）。 有关自动垃圾回收的开销的信息，请参阅[大型对象堆揭密](https://msdn.microsoft.com/magazine/cc534993.aspx)。
