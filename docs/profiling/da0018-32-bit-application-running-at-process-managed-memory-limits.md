---
title: DA0018：运行的 32 位应用程序达到了进程托管内存的限制 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.18
- vs.performance.DA0018
- vs.performance.rules.DA0018
ms.assetid: 98eb2d96-f92f-42f9-915c-e5ac2330ffbf
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: d7bebd25f499131b4beda109ebb9ac468c2435b1
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74780060"
---
# <a name="da0018-32-bit-application-running-at-process-managed-memory-limits"></a>DA0018：运行的 32 位应用程序达到了进程托管内存限制

|||
|-|-|
|规则 ID|DA0018|
|类别|分析工具使用情况|
|分析方法|采样|
|消息|托管内存分配接近 32 位进程的默认限制。 应用程序可能会受内存限制。|
|规则类型|警告|

 使用采样法、.NET 内存或资源争用方法进行分析时，必须收集至少 10 个样本才能触发此规则。

## <a name="cause"></a>原因
 在分析运行期间收集的系统数据表明：.NET Framework 内存堆接近托管堆在 32 位进程中可达到的最大大小。 此最大大小是默认值。 它以可分配给专用字节的进程地址空间总量为基础。 报告的值是分析进程处于活动状态时所观察到的最大堆值。 请考虑使用 .NET 内存分析方法再次进行分析，并优化应用程序对托管资源的使用。

 托管堆的大小接近默认限制时，将更频繁地调用自动垃圾回收进程。 这会增加内存管理开销。

 仅对 32 位计算机上运行的 32 位应用程序触发此规则。

## <a name="rule-description"></a>规则说明
 Microsoft .NET 公共语言运行时 (CLR) 提供自动内存管理机制，该机制使用垃圾回收器从应用程序不再使用的对象回收内存。 垃圾回收器是面向生成的，基于大量分配为短期分配的假设。 例如，局部变量应是短期的。 新创建的对象在 0 代中启动，如果在垃圾回收后它们仍然存在，则将提升到 1 代，如果应用程序仍使用它们，则最后将过渡到 2 代。

 会在大型对象堆上分配超过 85 KB 的托管对象，这样相比较小的对象，不会频繁对其进行垃圾回收和压缩。 大型对象是单独进行管理的，这是因为会假定大型对象更持久，并且将持久的大型对象与频繁分配的较小对象混合在一起会产生最差的堆碎片。

 托管堆总大小接近默认限制时，内存管理开销常会增加到一定程度，此时应用程序的响应情况和可伸缩性会开始受到影响。

## <a name="how-to-investigate-a-warning"></a>如何调查警告
 双击“错误列表”窗口中的消息，导航到[标记](../profiling/marks-view.md)视图。 查找 **.NET CLR Memory\\# Bytes in all Heaps** 和 **# Total committed bytes** 列。 确定是否存在特定阶段的程序执行，其中托管内存分配高于其他阶段。 比较 **# Bytes in all Heaps** 列的值与 **.NET CLR Memory\\# of Gen 0 Collections**、 **.NET CLR Memory\\# of Gen 1 Collections** 和 **.NET CLR Memory\\# of Gen 2 Collections** 列中报告的垃圾回收率，确定托管内存分配模式是否会影响垃圾回收率。

 在 .NET Framework 应用程序中，公共语言运行时会限制托管堆的总大小，使其略低于进程地址空间专用区域部分总大小的一半。 对于在 32 位计算机上运行的 32 位进程，进程地址空间专用部分的上限为 2 GB。 托管堆总大小开始接近其默认限制时，管理内存的开销可能会增加，应用程序的性能会降低。

 如果托管内存开销过多引发问题，请考虑采用以下任一选项：

- 优化应用程序对托管内存资源的使用情况

   -或-

- 采取措施以解除对 32 位进程虚拟内存最大大小的体系结构约束

  若要优化应用程序对托管内存资源的使用情况，请在 .NET 内存分配分析运行期间收集托管内存分配数据。 查看[.NET 内存数据视图](../profiling/dotnet-memory-data-views.md)报告，了解应用程序的内存分配模式。

  使用[对象生存期视图](../profiling/object-lifetime-view.md)确定哪些程序的数据对象可通过生成并在此被回收。

  使用[分配视图](../profiling/dotnet-memory-allocations-view.md)确定这些分配的执行路径。

  有关如何提高垃圾回收性能的详细信息，请参阅 MSDN 站点上的 .NET Framework 技术文章：[Garbage Collector Basics and Performance Hints](/previous-versions/dotnet/articles/ms973837(v=msdn.10))（垃圾回收器基础知识和性能提示）。

  若要解除对进程地址空间的专用部分大小的虚拟内存体系结构约束，请尝试在 64 位计算机上运行此 32 位进程。  64 位计算机上的 32 位进程最多可获得 4 GB 的专用虚拟内存。

  64 位计算机上运行的 64 位进程最多可获得 8 TB 的虚拟内存。 请考虑重新编译应用程序，将其作为本机 64 位应用程序执行。 此规则仅供参考，可能不需要采取纠正措施。
