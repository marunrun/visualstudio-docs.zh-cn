---
title: DA0022：第 2 代垃圾回收的速率很高 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.DA0022
- vs.performance.rules.DA0022
- vs.performance.22
ms.assetid: f871a547-0e6f-4b11-b2d7-174d30fc2ed8
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0dcfa4d3522d88b58e971c0a4ff3f27649c2d21b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "75844631"
---
# <a name="da0022-high-rate-of-gen-2-garbage-collections"></a>DA0022：第 2 代垃圾回收率高
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

规则 Id |DA0022 |  
|Category |。NET Framework 使用量 |  
|分析方法 |All |  
|消息 |发生第2代垃圾回收的速率相当高。 按设计来说，如果分配了大部分程序的数据结构且其保留时间较长，那么这通常并不是问题。 但是，如果此行为不在计划内，则表示应用程序可能锁定了对象。 如果不确定，可以收集 .NET 内存分配数据和对象生存期信息，便于了解应用程序使用的内存分配模式。|  
|规则类型 |警告 |  
  
 使用采样法、.NET 内存或资源争用方法进行分析时，必须收集至少 10 个样本才能触发此规则。  
  
## <a name="cause"></a>原因  
 分析期间收集的系统性能数据表明：与第 0 代和第 1 代垃圾回收相比，第 2 代垃圾回收中为 .NET Framework 对象回收的内存比例较高。  
  
## <a name="rule-description"></a>规则描述  
 Microsoft .NET 公共语言运行时 (CLR) 提供自动内存管理机制，该机制使用垃圾回收器从应用程序不再使用的对象回收内存。 垃圾回收器是面向生成的，基于大量分配为短期分配的假设。 例如，局部变量应是短期的。 新创建的对象在 0 代中启动，如果在垃圾回收后它们仍然存在，则将提升到 1 代，如果应用程序仍使用它们，则最后将过渡到 2 代。  
  
 收集 0 代中的对象时，通常频率和效率都较高。 收集 1 代中的对象时，通常频率和效率都较低。 最后，应以更低的频率收集 2 代中生存期较长的对象。 2 代回收是完整的垃圾回收运行，也是成本最高的操作。  
  
 第 2 代垃圾回收比例过高时将触发此规则。 运行良好的 .NET Framework 应用程序的第 1 代垃圾回收是第 2 代回收的 5 倍以上。 （理想值是 10 倍。）  
  
## <a name="how-to-investigate-a-warning"></a>如何调查警告  
 双击“错误列表”窗口中的消息，导航到分析数据的[标记视图](../profiling/marks-view.md)。 查找 **.NET CLR Memory\\# of Gen 0 Collections** 和 **.NET CLR Memory\\# of Gen 1 Collections** 列。 确定是否存在特定阶段的程序执行，其中垃圾回收更频繁。 将这些值与 **%Time in GC** 列进行比较，查看托管内存分配的模式是否会导致内存管理开销过多。  
  
 第 2 代垃圾回收比例较高并不总是表示有问题。 可能设计即是如此。 如果应用程序在执行期间分配必须长时间保持活跃状态的大型数据结构，则可能触发此规则。 此类应用程序存在内存压力时，可能会强制其频繁执行垃圾回收。 如果开销较低的 0 代和 1 代垃圾回收仅能回收少量托管内存，则将安排较为频繁的 2 代垃圾回收。  
  
 “标记”视图中存在有助于识别垃圾回收问题的其他 .NET CLR 内存列。 **%Time in GC** 列有助于了解当前的内存管理开销量。 如果应用程序通常使用相对较少的大型但持久的对象，则频繁的 2 代回收应该不会占用过多 CPU 时间。 如果应用程序因为需要更多物理内存 (RAM) 而产生内存压力，则还可能触发评估 **Memory\Pages/sec** 列值的相关规则。  
  
 若要了解应用程序的托管内存使用模式，请运行 .NET 内存分配分析再次进行分析，并选择对象生存期分析选项。  
  
 有关如何提高垃圾回收性能的信息，请参阅 Microsoft 网站上的 [Garbage Collector Basics and Performance Hints](https://msdn2.microsoft.com/library/ms973837.aspx)（垃圾回收器基础知识和性能提示）。 有关自动垃圾回收的开销的信息，请参阅[大型对象堆揭密](https://msdn.microsoft.com/magazine/cc534993.aspx)。
