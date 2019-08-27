---
title: .NET 内存数据视图 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .NET memory profiling method views
- profiling tools,.NET memory profiling views
ms.assetid: 79184d8e-769b-4ace-be2b-521147772081
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b1a866ba73669caba0c8d96647a134123f4ae753
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62970039"
---
# <a name="net-memory-data-views"></a>.NET 内存数据视图
本部分包含有关视图的参考信息以及包含 .NET 内存分析数据的探查器数据文件的报告。

## <a name="in-this-section"></a>本节内容
- [“摘要”视图](../profiling/summary-view-dotnet-memory-data.md)

 列出分配最多内存的函数和类型。

- [“分配”视图](../profiling/dotnet-memory-allocations-view.md)

 列出在分析运行期间分配的类型以及导致类型分配的调用关系树（执行路径）。

- [“对象生存期”视图](../profiling/object-lifetime-view.md)

 列出在分析运行期间分配的类型、实例的数目、大小（以字节为单位）和类型的垃圾回收生成。

- [“调用关系树”视图 - 采样](../profiling/call-tree-view-dotnet-memory-sampling-data.md)

 显示表示执行路径的层次结构树和分析运行期间函数的内存分配数据。

- [“模块”视图 - 采样](../profiling/modules-view-dotnet-memory-sampling-data.md)

 按模块组织 .NET 内存分配数据，并列出函数、源代码行和分配内存时所执行的说明。

- [“调用方/被调用方”视图 - .NET 内存采样数据](../profiling/caller-callee-view-dotnet-memory-sampling-data.md)

 列出所选函数的内存分配数据、调用所选函数的函数，以及所选函数调用的函数。

- [“函数”视图 - 采样](../profiling/functions-view-dotnet-memory-sampling-data.md)

 列出分析运行期间函数的内存分配数据。

- [“行”视图 - 采样](../profiling/lines-view-dotnet-memory-sampling-data.md)

 列出分析运行期间函数的源代码行的内存分配数据。

- [“指令指针”(IP) 视图 - 采样](../profiling/instruction-pointers-ips-view-dotnet-memory-sampling-data.md)

 列出分析运行期间函数指令的内存分配数据。

- [“调用关系树”视图 - 检测](../profiling/call-tree-view-dotnet-memory-instrumentation-data.md)

 显示表示执行路径的层次结构树、内存分配数据和分析运行期间已检测函数的详细计时数据。

- [“模块”视图 - 检测](../profiling/modules-view-dotnet-memory-instrumentation-data.md)

 按模块组织分析数据，并列出函数、内存分配数据和模块的详细计时信息。

- [“调用方/被调用方”视图 - .NET 内存检测数据](../profiling/caller-callee-view-net-memory-instrumentation-data.md)

 列出所选检测函数的内存分配数据和详细计时信息、调用所选函数的函数，以及所选函数调用的函数。

- [“函数”视图 - 检测](../profiling/functions-view-dotnet-memory-instrumentation-data.md)

 列出分析运行期间检测函数的内存分配数据。

## <a name="reference"></a>参考
- [“函数详细信息”视图](../profiling/function-details-view.md)

 显示所选函数和调用所选函数及被所选函数调用的函数之间的关系图形图表。

- [“进程”视图](../profiling/process-view.md)

 列出进程和线程的开始和结束时间。

- [“标记”视图](../profiling/marks-view.md)

 列出插入到分析数据文件的 ETW 和采样事件。

## <a name="related-sections"></a>相关章节
- [采样方法数据视图](../profiling/profiler-sampling-method-data-views.md)

 关于使用采样方法生成的探查器数据文件的视图和报表的参考信息。

- [检测方法数据视图](../profiling/instrumentation-method-data-views.md)

 关于使用检测方法生成的探查器数据文件的视图和报表的参考信息。