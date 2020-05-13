---
title: 了解性能收集方法 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.wizard.methodpage
helpviewer_keywords:
- Profiling Tools, profiling methods
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: ad451c6146593713b02901ac43423c76174d0684
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74778084"
---
# <a name="understand-performance-collection-methods"></a>了解性能收集方法

Visual Studio 分析工具提供了五种可以用于收集性能数据的方法。 本主题介绍了不同方法，并提供了一些适合使用特定方法收集数据的建议方案。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

|方法|描述|
|------------|-----------------|
|[采样](#sampling)|收集有关应用程序执行的工作的统计数据。|
|[检测](#instrumentation)|收集有关每个函数调用的详细计时信息。|
|[并发](#concurrency)|收集有关多线程应用程序的详细信息。|
|[.NET 内存](#net-memory)|收集有关 .NET 内存分配和垃圾回收的详细信息。|
|[层交互](#tier-interaction)|收集有关对 SqlServer 数据库的同步 ADO.NET 函数调用的信息。<br /><br /> 可以使用任何版本的 Visual Studio 收集层交互分析。 但是，层交互分析数据只能在 Visual Studio Enterprise 中查看。|

通过使用一些分析方法，还可以收集其他数据，如软件和硬件性能计数器。 有关详细信息，请参阅[收集其他性能数据](../profiling/collecting-additional-performance-data.md)。

## <a name="sampling"></a>采样

采样分析方法收集有关应用程序在分析运行过程中执行的工作的统计数据。 采样方法是轻量级的，对应用程序方法的执行几乎没有什么影响。

采样是 Visual Studio 分析工具的默认方法。 它可用于以下情况：

- 对应用程序性能的初步研究。
- 调查涉及处理器 (CPU) 使用率的性能问题。

采样分析方法按设置的间隔中断计算机处理器并收集函数调用堆栈。 对于正在执行的函数会递增独占样本计数，对于调用堆栈上的所有调用函数会递增非独占计数。 采样报告会对分析的模块、函数、源代码行和指令显示这些计数的总和。

默认情况下，探查器将采样间隔设置为 CPU 周期。 可以将间隔类型更改为其他 CPU 性能计数器，并且可以为间隔设置计数器事件数。 还可以收集层交互分析 (TIP) 数据，这些数据可提供有关通过 ADO.NET 对 SQL Server 数据库进行的查询的信息。

[通过采样收集性能统计信息](../profiling/collecting-performance-statistics-by-using-sampling.md)

[了解采样数据值](../profiling/understanding-sampling-data-values.md)

[示例方法数据视图](../profiling/profiler-sampling-method-data-views.md)

## <a name="instrumentation"></a>检测

检测分析方法为分析的应用程序中的函数调用收集详细计时。 检测分析可用于以下情况：

- 调查输入/输出瓶颈（如磁盘 I/O）。
- 对特定模块或函数集的仔细检查。

检测方法会将代码注入到一个二进制文件中，该文件会为检测的文件中的每个函数以及这些函数进行的每个函数调用捕获计时信息。 检测还会确定函数何时调入以进行操作（如对文件进行写入）。 检测报告使用四个值表示在函数或源代码行中所用的总时间：

- 已用非独占 - 执行函数或源行所用的总时间。

- 应用程序非独占 - 执行函数或源行所用的时间，但不包括在操作系统调用中所用的时间。

- 已用独占 - 在函数或源代码行的体中执行代码所用的时间。 不包括执行函数或源行调用的函数所用的时间。

- 应用程序独占 - 在函数或源代码行的体中执行代码所用的时间。 不包括执行操作系统调用所用的时间以及执行函数或源行调用的函数所用的时间。

还可以使用检测方法收集 CPU 和软件性能计数器。

[了解检测数据值](../profiling/understanding-instrumentation-data-values.md)

[通过检测收集详细计时数据](../profiling/collecting-detailed-timing-data-by-using-instrumentation.md)

[检测方法数据视图](../profiling/instrumentation-method-data-views.md)

## <a name="concurrency"></a>并发

并发分析收集有关多线程应用程序的信息。 资源争用分析收集每次争用线程被迫等待访问共享资源时的详细调用堆栈信息。 并发可视化还收集有关多线程应用程序如何与自己、硬件、操作系统和主计算机上的其他进程进行交互的更多常规信息：

- 资源争用报告显示争用的总数，以及对于在其中发生等待的模块、函数、源代码行和指令，等待资源所用的总时间。 时间线关系图也会在争用发生时显示争用。

- 并发可视化工具会显示图形信息，可以使用这些信息查找性能瓶颈、CPU 利用率不足、线程争用、线程迁移、同步延迟、I/O 重叠区域和其他信息。 如果可能，图形输出会链接到调用堆栈和源代码数据。 只能为命令行和 Windows 应用程序收集并发可视化数据。

[了解资源争用数据值](../profiling/understanding-resource-contention-data-values.md)

[收集线程和进程并发数据](../profiling/collecting-thread-and-process-concurrency-data.md)

[资源争用数据视图](../profiling/resource-contention-data-views.md)

[并发可视化工具](../profiling/concurrency-visualizer.md)

## <a name="net-memory"></a>.NET 内存

.NET 内存分配分析方法在分析的应用程序中每次分配 .NET Framework 对象时都中断计算机处理器。 同时收集对象生存期数据时，探查器会在每个 .NET Framework 垃圾回收之后中断处理器。

探查器收集有关在分配中创建的对象或在垃圾回收中销毁的对象的类型、大小和数量的信息。

- 分配事件发生时，探查器收集有关函数的调用堆栈的其他信息。 对于当前正在执行的函数会递增独占分配计数，对于调用堆栈上的所有调用函数会递增非独占计数。 .NET 报告会对分析的类型、模块、函数、源代码行和指令显示这些计数的总和。

- 垃圾回收发生时，探查器收集有关销毁的对象的数据以及有关每一代垃圾回收中的对象的信息。 在分析运行结束时，探查器会记录有关未显式销毁的对象的数据。 对象生存期报告显示在分析运行中分配的每种类型的总计。

.NET 内存分析可以在采样或检测模式下使用。 选择的模式不会影响分配和对象生存期报告，它们对于 .NET 内存分析是唯一的：

- 在采样模式下运行 .NET 内存分析时，探查器 .NET 会将内存分配事件用作间隔，并将分配的对象数和分配的总字节数在报告中显示非独占和独占值。

- 在检测模式下运行 .NET 内存分析时，会收集详细计时信息以及非独占和独占分配值。

[了解内存分配和对象生存期数据值](../profiling/understanding-memory-allocation-and-object-lifetime-data-values.md)

[收集 .NET 内存分配和生存期数据](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)

[.NET 内存数据视图](../profiling/dotnet-memory-data-views.md)

## <a name="tier-interaction"></a>层交互

层交互分析将有关 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 页面或其他应用程序与 [!INCLUDE[ssNoVersion](../data-tools/includes/ssnoversion_md.md)] 数据库之间的同步 [!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)] 调用的信息添加到分析数据文件。 这些数据包括调用的数量和时间，以及最大和最小次数。 层交互数据可以添加到使用采样、检测、.NET 内存或并发方法收集的分析数据。

![层交互分析数据](../profiling/media/tierinteraction_profilingtools.png "TierInteraction_ProfilingTools")

通过分析工具收集的层交互数据

[收集层交互数据](../profiling/collecting-tier-interaction-data.md)

[层交互视图](../profiling/tier-interaction-views.md)

## <a name="see-also"></a>请参阅

[如何：收集网站性能数据](../profiling/how-to-collect-performance-data-for-a-web-site.md)
[性能分析初学者指南](../profiling/beginners-guide-to-performance-profiling.md)
