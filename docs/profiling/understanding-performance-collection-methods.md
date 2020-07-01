---
title: 了解性能收集方法 | Microsoft Docs
ms.date: 4/30/2020
ms.topic: conceptual
f1_keywords:
- vs.performance.wizard.methodpage
helpviewer_keywords:
- Profiling tools, profiling methods
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 0a37d58d1bd18ef19f610602ec8f2238816405e4
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285746"
---
# <a name="understand-performance-collection-methods"></a>了解性能收集方法

Visual Studio 分析工具提供了五种用于收集性能数据的方法。 本文介绍了不同方法，并提供了一些适合使用特定方法收集数据的建议方案。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能要求对 Visual Studio 探查器在这些平台上收集数据的方式做出重大变更。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

|方法|描述|
|------------|-----------------|
|[采样](#sampling)|收集有关应用执行的工作的统计数据。|
|[检测](#instrumentation)|收集有关每个函数调用的详细计时信息。|
|[并发](#concurrency)|收集有关多线程应用的详细信息。|
|[.NET 内存](#net-memory)|收集有关 .NET 内存分配和垃圾回收的详细信息。|
|[层交互](#tier-interaction)|收集有关对 SQL Server 数据库的同步 ADO.NET 函数调用的信息。<br /><br /> 任何版本的 Visual Studio 都可以收集层交互分析数据。 但是，只能在 Visual Studio Enterprise 中查看该数据。|

通过使用一些分析方法，还可以收集其他数据，如软件和硬件性能计数器。 有关详细信息，请参阅[收集其他性能数据](../profiling/collecting-additional-performance-data.md)。

## <a name="sampling"></a>采样

采样分析方法收集有关应用在分析运行过程中执行的工作的统计数据。 采样方法是轻量级的，对应用方法的执行几乎没有什么影响。

采样是 Visual Studio 分析工具的默认方法。 这有助于完成以下任务：

- 对应用性能的初步研究
- 调查涉及微处理器 (CPU) 使用率的性能问题

采样分析方法按设置的间隔中断计算机 CPU 并收集函数调用堆栈。 对正在运行的函数递增独占采样计数。 对调用堆栈上的所有调用函数递增非独占计数。 采样报告会对分析的模块、函数、源代码行和指令显示这些计数的总和。

默认情况下，探查器将采样间隔设置为 CPU 周期。 可以将间隔类型更改为其他 CPU 性能计数器，或者为间隔设置计数器事件数。 还可以收集层交互分析 (TIP) 数据。 此数据提供有关通过 ADO.NET 对 SQL Server 数据库进行的查询的信息。

[通过采样收集性能统计信息](../profiling/collecting-performance-statistics-by-using-sampling.md)

[了解采样数据值](../profiling/understanding-sampling-data-values.md)

[示例方法数据视图](../profiling/profiler-sampling-method-data-views.md)

## <a name="instrumentation"></a>检测

检测分析方法为分析的应用中的函数调用收集详细计时。 检测分析有助于完成以下任务：

- 调查输入/输出瓶颈（如磁盘 I/O）
- 仔细检查特定模块或函数集

检测方法将代码注入到二进制文件中。 此代码捕获检测文件中所有函数的计时信息，以及这些函数进行的每个函数调用。 检测还会确定何时对操作系统调用函数，以执行诸如写入文件之类的操作。

检测报告使用下列四个值表示在函数或源代码行中所用的总时间：

- 已用非独占 - 运行函数或源代码行所用的总时间。

- 应用程序非独占 - 运行函数或源代码行所用的时间。 不包括对操作系统的调用。

- 已用独占 - 运行函数或源代码行所用的时间。 不包括对其他函数的调用。

- 应用程序独占 - 运行函数或源代码行所用的时间。 不包括对操作系统或其他函数的调用。

还可以使用检测方法收集 CPU 和软件性能计数器。

[了解检测数据值](../profiling/understanding-instrumentation-data-values.md)

[通过检测收集详细计时数据](../profiling/collecting-detailed-timing-data-by-using-instrumentation.md)

[检测方法数据视图](../profiling/instrumentation-method-data-views.md)

## <a name="concurrency"></a>并发

并发分析收集有关多线程应用的信息。 每当争用线程等待访问共享资源时，资源争用分析都会收集详细的调用堆栈信息。 并发可视化还收集有关多线程应用如何与以下对象进行交互的更多常规信息：

  - 本身。
  - 硬件。
  - 操作系统。
  - 主计算机上的其他进程。

资源争用报告显示争用的总次数。 它们还报告模块、函数、源代码行和指令等待资源的总时间。 时间线关系图会在争用发生时显示争用。

并发可视化工具显示关系图信息以帮助你查找：

  - 性能瓶颈。
  - CPU 使用不足。
  - 线程争用。
  - 线程迁移。
  - 同步延迟。
  - 重叠 I/O 区域。

  如果可能，图形输出会链接到调用堆栈和源代码中的数据。 只能为命令行应用和 Windows 应用收集并发可视化数据。

[了解资源争用数据值](../profiling/understanding-resource-contention-data-values.md)

[收集线程和进程并发数据](../profiling/collecting-thread-and-process-concurrency-data.md)

[资源争用数据视图](../profiling/resource-contention-data-views.md)

[并发可视化工具](../profiling/concurrency-visualizer.md)

## <a name="net-memory"></a>.NET 内存

.NET 内存分配分析方法在分析的应用中每次分配 .NET Framework 对象时都中断 CPU。 同时收集对象生存期数据时，探查器会在每个 .NET Framework 垃圾回收之后中断 CPU。

探查器收集有关在分配中创建的对象或在垃圾回收中销毁的对象的类型、大小和数量的信息。

- 分配事件发生时，探查器收集有关函数的调用堆栈的其他信息。 探查器会递增当前正在运行的函数的独占分配计数。 它还会递增调用堆栈上所有调用函数的非独占计数。 .NET 报告会对分析的类型、模块、函数、源代码行和指令显示这些计数的总和。

- 垃圾回收发生时，探查器收集有关销毁的对象以及每一代垃圾回收中的对象的数据。 在分析运行结束时，探查器会记录有关未显式销毁的对象的数据。 对象生存期报告显示在分析运行中分配的每种类型的总计。

.NET 内存分析可以在采样模式或检测模式下使用。 选择的模式不会影响分配和对象生存期报告，它们对于 .NET 内存分析是唯一的。

- 在采样模式下运行 .NET 内存分析时，探查器将使用内存分配事件作为间隔。 它还会将分配的对象和字节的总数显示为报告中的非独占值和独占值。

- 在检测模式下运行 .NET 内存分析时，探查器会收集详细计时信息以及非独占和独占分配值。

[了解内存分配数据值和对象生存期数据值](../profiling/understanding-memory-allocation-and-object-lifetime-data-values.md)

[收集 .NET 内存分配和生存期数据](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)

[.NET 内存数据视图](../profiling/dotnet-memory-data-views.md)

## <a name="tier-interaction"></a>层交互

层交互分析将有关 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 页面或其他应用与 [!INCLUDE[ssNoVersion](../data-tools/includes/ssnoversion_md.md)] 数据库之间的同步 [!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)] 调用的信息添加到分析数据文件。 这些数据包括调用的数量和时间，以及最大和最小次数。 可以将层交互数据添加到使用采样、检测、.NET 内存或并发方法收集的分析数据。

![层交互分析数据流](../profiling/media/tierinteraction_profilingtools.png "层交互分析数据流")

有关分析工具收集的层交互数据的信息，请参阅以下文章。

[收集层交互数据](../profiling/collecting-tier-interaction-data.md)

[层交互视图](../profiling/tier-interaction-views.md)

## <a name="see-also"></a>请参阅

[如何：收集网站性能数据](../profiling/how-to-collect-performance-data-for-a-web-site.md)

[性能分析初学者指南](../profiling/beginners-guide-to-performance-profiling.md)
