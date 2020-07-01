---
title: 同时使用多个探查器工具 | Microsoft Docs
ms.date: 4/29/2020
ms.topic: how-to
helpviewer_keywords:
- Profiler, multiple tools
author: Sagar-S-S
ms.author: sashe
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: f72757d46496c3990c0a0d4205753d185078eac7
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332040"
---
# <a name="using-multiple-profiler-tools-simultaneously"></a>同时使用多个探查器工具

性能探查器的设计理念是，可以在同一会话中使用多个工具来帮助了解性能问题。 性能探查器中的大部分工具都支持并发运行，如 [CPU 使用情况](../profiling/cpu-usage.md)、[.NET Async 工具](../profiling/analyze-async.md)和[数据库](../profiling/analyze-database.md)工具。 若要在同一诊断会话中同时运行工具，请单击其旁边的复选框，然后启动诊断会话。

![诊断中心“所有工具”已选中](../profiling/media/diaghuballtoolsselected.png "诊断中心“所有工具”已选中")

>[!NOTE]
>某些工具（如 [.NET 对象分配](../profiling/dotnet-alloc-tool.md)工具）不能与其他工具一起运行，因为它们的开销较大或存在其他技术限制。

## <a name="time-filtering"></a>时间筛选 

在分析过程中，时间筛选操作在各种工具中应用，因此，你可以使用一个工具中的信息来缩小时间范围并在另一工具中筛选数据。 此功能有助于将分析引导到跟踪中的特定点，并帮助你了解应用程序的状态。

![诊断中心时间筛选](../profiling/media/diaghubtimefiltering.png "诊断中心时间筛选")

## <a name="see-also"></a>请参阅

- [优化探查器设置](../profiling/optimize-profiler-settings.md)
- [运行带或不带调试器的分析工具](../profiling/running-profiling-tools-with-or-without-the-debugger.md)
- [了解性能收集方法](../profiling/understanding-performance-collection-methods-perf-profiler.md)
