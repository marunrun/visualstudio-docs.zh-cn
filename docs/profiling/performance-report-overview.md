---
title: 性能报告概述 | Microsoft 文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, about performance rerports
- performance, reports
- performance reports, about performance reports
ms.assetid: 7324c24c-fd09-479b-b2ad-e0c3b613e040
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 517156677a6d3711fa5dc2e4a15629a55229cfe2
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74772227"
---
# <a name="performance-report-overview"></a>性能报告概述
在 Visual Studio Team System Development Edition 集成开发环境 (IDE) 的“性能报告”  窗口中，可以查看性能会话的分析数据。 分析数据保存在 .vsp 和 .vsps 文件中。 报告视图窗口可用于查看和分析应用程序性能问题。

> [!CAUTION]
> 分析数据文件包含敏感信息，如计算机名、操作系统的版本、文件路径、内存信息和其他计算机设置信息。 无论是采用本机 .vsp 格式，还是导出到 .csv 或 .xml 文件时，都应对数据的分发保持严格控制    。
>
> 如果在性能会话期间收集事件跟踪数据，则事件跟踪日志 (.etl) 文件中可能会出现其他信息  。 此信息包括域和用户名；因此，应对日志文件的分发保持严格控制。

## <a name="performance-report-window"></a>“性能报告”窗口
 “性能报告”窗口是一个工具窗口，用于查看、管理和筛选性能数据，包含可自定义查询控制。

 在“性能报告”窗口的主工具栏上，可以访问每个视图。 单击“当前视图”  列表旁的箭头可显示并选择可用的各个视图。

 “性能报告”窗口提供以下数据视图：

### <a name="summary-view"></a>“摘要”视图
 默认情况下，分析数据会显示在“摘要”视图中。 此视图是调查性能问题的起点。 在“摘要”视图的每行中，可以通过右键单击函数或模块名来移动到更详细的视图。 有关详细信息，请参阅[“摘要”视图](../profiling/summary-view.md)。

### <a name="callercallee-view"></a>“调用方/被调用方”视图
 “调用方/被调用方”视图显示单个函数的调用树。 该视图划分为三个部分：

- 目标函数显示在视图中间。

- 调用该函数的函数（调用方）显示在目标函数上方。

- 目标函数调用的函数（被调用方）显示在目标下方。

  可以通过在调用方列表或被调用方列表中双击任何函数来选择不同的函数。 有关详细信息，请参阅[“调用方/被调用方”视图](../profiling/caller-callee-view.md)。

### <a name="call-tree-view"></a>“调用关系树”视图
 “调用关系树”视图显示在分析应用程序中遍历的函数执行路径。 树的根是应用程序或组件的入口点。 每个函数节点都列出它调用的所有函数以及有关这些函数调用的性能数据。

 “调用关系树”视图还可以展开以及突出显示消耗了最多时间或采样频率最高的函数的执行路径。 若要显示最活跃的路径，请右键单击函数，然后单击“展开热路径”  。 有关详细信息，请参阅[“调用关系树”视图](../profiling/call-tree-view.md)。

### <a name="process-view"></a>“进程”视图
 “进程”视图显示进行分析的每个进程和线程的性能数据。 有关详细信息，请参阅[“进程”视图](../profiling/process-view.md)。

### <a name="modules-view"></a>“模块”视图
 “模块”视图列出项目中的模块，并呈现每个模块的分析数据。 展开或折叠模块名可显示函数分析数据。 使用采样收集数据时，还会提供源代码行和指令指针分析数据。 有关详细信息，请参阅[“模块”视图](../profiling/modules-view.md)。

### <a name="functions-view"></a>“函数”视图
 “函数”视图列出分析过程中调用的函数。 有关详细信息，请参阅[“函数”视图](../profiling/functions-view.md)。

### <a name="line-view"></a>“行”视图
 “行”视图可用于查看在采样分析过程中执行的特定源代码行。 有关详细信息，请参阅[“行”视图](../profiling/lines-view.md)。

### <a name="instruction-pointer-ip-view"></a>“指令指针”(IP) 视图
 “指令指针”视图可用于查看在采样分析过程中执行的特定指令。 有关详细信息，请参阅[“指令指针”(IP) 视图](../profiling/instruction-pointers-ips-view.md)。

### <a name="allocation-view"></a>“分配”视图
 如果在“性能会话”  属性对话框的“常规”  页上选择了“收集 .NET 对象分配”  ，则可使用“分配”视图。 请参阅[性能会话概述](../profiling/performance-session-overview.md)。 “分配”视图列出应用程序或组件分配的 .NET 对象。 展开某个对象行时，会显示调用树。 调用树显示对象创建所产生的执行路径。 还会在调用树中显示有关每个函数的非独占和独占分配数量的信息。 “分配”视图还可以展开以及突出显示分配了最大对象数的函数的执行路径。 若要显示最活跃的路径，请右键单击函数，然后单击“展开热路径”  。 有关详细信息，请参阅[收集 .NET 内存分配数据和生存期数据](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)和[“分配”视图](../profiling/dotnet-memory-allocations-view.md)。

### <a name="objects-lifetime-view"></a>“对象生存期”视图
 如果在“性能会话”  属性对话框的“常规”  页上选择了“收集 .NET 对象分配信息”  和“同时收集 .NET 对象的生存期信息”  ，则可使用“对象生存期”视图。

 “对象生存期”视图显示每种类型的实例的总数，以及在每代垃圾回收中收集的对象的数量。 有关详细信息，请参阅[“对象生存期”视图](../profiling/object-lifetime-view.md)。

## <a name="customizable-filter-control"></a>可自定义筛选器控件
 可自定义筛选器控件具有以下选项：

- **导入筛选器** - 检索以前保存的自定义查询。

- **导出筛选器** - 将自定义查询保存到指定位置。

- **执行查询** - 运行在自定义查询控件中显示的查询。

- **停止查询** - 停止正在运行的查询的执行。 如果没有查询正在运行，则此按钮不可用。

- **显示查询** - 显示/隐藏自定义查询控件。

- **保存分析结果** - 将报告及其当前分析保存为 .vsps 文件。

- **导出** - 将当前报告保存在 .CVS 格式或 .XML 格式文件中（可以选择保存不同的视图）。

## <a name="see-also"></a>请参阅
- [分析性能工具数据](../profiling/analyzing-performance-tools-data.md)
- [性能报告视图](../profiling/performance-report-views.md)
