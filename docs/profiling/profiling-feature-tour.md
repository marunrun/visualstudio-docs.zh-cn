---
title: 使用分析工具衡量性能
description: 简要了解 Visual Studio 中提供的各种诊断工具。
ms.custom: mvc
ms.date: 06/03/2020
ms.topic: quickstart
helpviewer_keywords:
- diagnostic tools
ms.assetid: d2ee0301-ea78-43d8-851a-71b7b2043d73
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 89006ab582a48f7f3be54b4eb459903b64af7daf
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85280224"
---
# <a name="quickstart-first-look-at-profiling-tools"></a>快速入门：首先了解分析工具

Visual Studio 提供了各种分析工具，可依据你的应用类型帮助你诊断不同种类的性能问题。 在本文中，我们将简要介绍最常见的分析工具。

## <a name="view-performance-while-debugging"></a>调试时查看性能

调试会话期间可以访问的分析工具在“诊断工具”窗口中提供。 将自动显示“诊断工具”窗口，除非你已将其关闭。 若要显示该窗口，请依次单击“调试”、“Windows”、“显示诊断工具”。 窗口打开后，可以选择想要用于收集数据的工具。

![“诊断工具”窗口](../profiling/media/prof-tour-diagnostic-tools.png "诊断工具")

调试时，你可以使用“诊断工具”窗口分析 CPU 和内存使用情况，并且可以查看显示性能相关信息的事件。

![诊断工具“摘要”视图](../profiling/media/prof-tour-cpu-and-memory-graph.gif "诊断工具“摘要”视图")

“诊断工具”窗口是探查应用的常见方式，但对于版本生成，也可改为对应用执行事后分析。 有关不同方法的详细信息，请参阅[运行带或不带调试器的分析工具](../profiling/running-profiling-tools-with-or-without-the-debugger.md)。 若要了解不同应用类型对应的探查工具支持，请参阅[我应使用哪个工具？](#which-tool-should-i-use)。

> [!NOTE]
> 可以在 Windows 7 及更高版本中使用事后分析工具。 要运行带调试器的分析工具（“诊断工具”窗口），需具备 Windows 8 及更高版本。

## <a name="examine-performance-using-perftips"></a>使用 PerfTips 检查性能

通常，查看性能信息的最简单方法是使用 [PerfTips](../profiling/perftips.md)。 使用 PerfTips，可以在与代码交互时查看性能信息。 你可以查看事件持续时间（从调试程序上次暂停或应用启动时开始计算）等信息。 例如，如果单步执行代码（F10、F11），PerfTips 将显示自上次单步执行操作到当前单步执行操作的应用运行时持续时间。

![分析简介性能提示](../profiling/media/prof-tour-perf-tips.png "分析简介性能提示")

使用 PerfTips 可以检查执行代码块所用的时间，也可以检查完成单个函数所需的时间。

PerfTips 与诊断工具的“事件”视图显示相同的事件。 在“事件”视图中，可以查看调试时发生的不同事件，例如设置断点或代码单步执行操作。

![诊断工具“事件”视图](../profiling/media/prof-tour-events.png "诊断工具“查看事件”")

 > [!NOTE]
 > 如果你有 Visual Studio Enterprise，你还可以在此选项卡中查看 [IntelliTrace 事件](../debugger/intellitrace.md)。

## <a name="analyze-cpu-usage"></a>分析 CPU 的使用量

CPU 使用率工具很适合用于开始分析应用的性能。 它将向你详细介绍应用正在使用的 CPU 资源。 有关 CPU 使用率工具的更详细演练，请参阅[通过分析 CPU 使用情况衡量应用程序性能](../profiling/beginners-guide-to-performance-profiling.md)。

在诊断工具的“摘要”视图中，选择“启用 CPU 分析”（必须正在参与调试会话）。

![诊断工具中的“启用 CPU 使用率”](../profiling/media/prof-tour-enable-cpu-profiling.png "诊断工具“启用 CPU 使用率”")

使用该工具的一种方法是在代码中设置两个断点，一个在开头，一个在函数的末尾或想要分析的代码区域。 在第二个断点暂停时，请检查分析数据。

“CPU 使用率”视图显示按最长运行时间排序的函数列表，运行时间最长的函数排在前面。 这有助于将你引导至发生性能瓶颈的函数。

![诊断工具“CPU 使用率”视图](../profiling/media/prof-tour-cpu-usage.png "诊断工具“CPU 使用率”")

双击感兴趣的函数，然后将看到更加详细的三窗格“蝶形”视图，其中所选函数位于窗口中央，调用函数位于左侧，而被调用函数位于右侧。 **函数体**部分显示函数体中所用的时间总量（及百分比），其中不包括调用和被调用函数中所用的时间。 此数据可以帮助评估函数本身是否属于性能瓶颈。

![诊断工具调用方和被调用方“蝶形”视图](../profiling/media/prof-tour-cpu-usage-caller-callee.png "诊断工具“调用方和被调用方”视图")

## <a name="analyze-memory-usage"></a>分析内存使用情况

借助“诊断工具”窗口，你还可以使用“内存使用情况”工具来评估应用中的内存使用情况 。 例如，你可以查看堆上对象的数量和大小。 要更详细了解地如何分析内存，请参阅[分析内存使用情况](../profiling/memory-usage.md)。 另一种内存分析工具 [.NET 对象分配工具](../profiling/dotnet-alloc-tool.md)可帮助确定 .NET 代码中的分配模式和异常。

若要使用集成了调试器的内存使用情况工具分析内存使用情况，则需要拍摄至少一张内存快照。 通常，分析内存的最好方法是拍摄两张快照；一张正好拍摄于发生可疑内存问题之前，另一张拍摄于发生可疑内存问题之后。 然后可以查看两张快照的差异，并发现实际更改的内容。

![诊断工具中的“获取快照”](../profiling/media/prof-tour-take-snapshots.gif "诊断工具“获取快照”")

选择其中一个箭头链接时，系统会提供关于堆的差异视图（一个向上的红色箭头![内存使用量增加](../profiling/media/prof-tour-mem-usage-up-arrow.png "内存使用量增加")表明对象计数（左）增加或堆大小（右）增加）。 如果单击右侧的链接，将获得按堆大小增加最多的对象进行排序的差异堆视图。 这可帮助查明内存问题。 例如，在下图中，`ClassHandlersStore` 对象使用的字节数在第二张快照中增加了 3,492 字节。

![诊断工具“堆差异”视图](../profiling/media/prof-tour-mem-usage-diff-heap.png "诊断工具“堆差异”视图")

如果改为单击“内存使用量”视图左侧的链接，堆视图将按对象计数排列；数量增加最多的特殊类型的对象显示在顶部（按“计数差异”列排序）。

## <a name="profile-release-builds-without-the-debugger"></a><a name="post_mortem"></a>不使用调试器分析发行版本

CPU 使用率和内存使用量等分析工具可与调试器配合使用（见前文），你也可事后使用性能探查器运行分析工具，其的是就发行版本进行分析。 在性能探查器中，可以在应用仍在运行时收集诊断信息，然后在应用停止后检查收集的信息。 有关这些不同方法的详细信息，请参阅[运行带或不带调试器的分析工具](../profiling/running-profiling-tools-with-or-without-the-debugger.md)。 在性能探查器中也可以使用其他工具（如 [.NET 对象分配工具](../profiling/dotnet-alloc-tool.md)）。

![性能探查器](../profiling/media/prof-tour-performance-profiler.png "性能探查器")

选择“调试” > “性能探查器”（或按 Alt + F2）以打开性能探查器。

该窗口使你能够在某些应用场景中选择[多个分析工具](../profiling/use-multiple-profiler-tools-simultaneously.md)。 CPU 使用率等工具可提供在分析中有所帮助的补充性数据。 还可以使用[命令行探查器](../profiling/profile-apps-from-command-line.md)以启用涉及多个分析工具的方案。

## <a name="analyze-resource-consumption-xaml"></a>分析资源消耗情况 (XAML)

在 XAML 应用（例如 Windows 桌面 WPF 应用和 UWP 应用）中，可以使用应用程序时间线工具分析资源消耗情况。 例如，你可以分析应用程序准备 UI 框架（布局和呈现）以及为网络和磁盘请求提供服务所花费的时间，以及在应用程序启动、页面加载以及调整窗口大小等应用场景中花费的时间。 若要使用该工具，请在性能探查器中选择“应用程序时间线”，然后选择“开始”。 在应用中，浏览资源消耗存在可疑问题的应用场景，然后选择“停止收集”生成报表。

**可视吞吐量**关系图中的帧速率低可能对应运行应用时看到的视觉问题。 与此类似，**UI 线程使用率**关系图中的高数值也可能对应 UI 响应能力问题。 在报表中，你可以选择出现可疑性能问题的时间段，然后在“时间线”详细信息视图（下方窗格）中检查详细的 UI 线程活动。

![应用程序时间线分析工具](../profiling/media/prof-tour-application-timeline.gif "分析简介应用程序时间线")

在时间线详细信息视图中，可以找到活动类型（或涉及的 UI 元素）以及活动持续时间等信息。 例如，在图中，网格控件的**布局**事件需要 57.53 毫秒。

有关详细信息，请参阅[应用程序时间线](../profiling/application-timeline.md)。

::: moniker range=">=vs-2019"

## <a name="examine-application-events"></a>检查应用程序事件

使用通用[事件查看器](../profiling/events-viewer.md)，可以通过事件列表（如模块加载、线程启动和系统配置）查看应用程序的活动，以帮助更好地诊断应用程序在 Visual Studio 探查器中的执行情况。 此工具在性能探查器中提供。 选择“调试” > “性能探查器”（或按 Alt + F2）以打开性能探查器。

该工具在列表视图中显示每个事件。 列提供有关每个事件的信息，例如事件名称、时间戳和进程 ID。

![事件查看器跟踪](../profiling/media/eventviewertrace.png "事件查看器跟踪")

## <a name="analyze-asynchronous-code-net"></a>分析异步代码 (.NET)

[.NET 异步工具](../profiling/analyze-async.md)使你可以分析应用程序中异步代码的性能。 此工具在性能探查器中提供。 选择“调试” > “性能探查器”（或按 Alt + F2）以打开性能探查器。

该工具在列表视图中显示每个异步操作。 可以查看信息，如异步操作的开始时间、结束时间和总时间。

![.NET Async 工具已停止](../profiling/media/async-tool-opened.png ".NET Async 工具已停止")

## <a name="analyze-database-performance-net-core"></a>分析数据库性能 (.NET Core)

对于使用 ADO.NET 或 Entity Framework Core 的 .NET Core 应用，可以使用[数据库工具](../profiling/analyze-database.md)记录应用程序在诊断会话期间所进行的数据库查询。 然后，你可以分析各个查询的相关信息，以找到应用性能可改进的地方。 此工具在性能探查器中提供。 选择“调试” > “性能探查器”（或按 Alt + F2）以打开性能探查器。

该工具在列表视图中显示每个查询。 可以查看查询开始时间和持续时间等信息。

Allocation![](./media/db-gotosource.png "分配")

::: moniker-end

## <a name="examine-ui-performance-and-accessibility-events-uwp"></a>检查 UI 性能和可访问性事件 (UWP)

在 UWP 应用中，可在“诊断工具”窗口中启用“UI 分析” 。 该工具搜索常见的性能和辅助功能问题，在你进行调试时将其显示在“事件”视图中。 事件描述可提供有助于解决问题的信息。

![诊断工具中的“视图 UI 分析事件”](../profiling/media/prof-tour-ui-analysis.png "诊断工具“视图 UI 分析事件”")

## <a name="analyze-gpu-usage-direct3d"></a>分析 GPU 使用情况 (Direct3D)

在 Direct3D 应用（Direct3D 组件必须使用 C++）中，你可以检查关于 GPU 的活动并分析性能问题。 有关详细信息，请参阅 [GPU 使用情况](/visualstudio/debugger/graphics/gpu-usage)。 若要使用该工具，请在性能探查器中选择“GPU 使用情况”，然后选择“开始”。 在应用中，浏览你对分析感兴趣的应用场景，然后选择“停止收集”生成报表。

在关系图中选择一个时间段，并选择“查看详细信息”后，下方窗格中将出现详细信息视图。 在详细信息视图中，你可以检查每个 CPU 和 GPU 上发生活动的数量。 选择底部窗格中的事件可在时间线中获得弹出窗口。 例如，选择 **Present** 事件可查看 **Present** 调用弹出窗口。 （浅灰色垂直 Vsync 线条可以作为参考，用于了解某些 **Present** 是否调用缺少的 Vsync。 为了让应用稳定达到 60 FPS，每两个 Vsync 之间必须有一个 **Present** 调用。）

![GPU 使用情况分析工具](../profiling/media/prof-tour-gpu-usage.png "诊断 GPU 使用情况")

关系图还可用于确定是否存在与 CPU 或 GPU 绑定的性能瓶颈。

::: moniker range="vs-2017"
## <a name="analyze-performance-javascript-uwp"></a>分析性能 (JavaScript UWP)

对于 UWP 应用，可以使用“JavaScript 内存”工具和“HTML UI 响应能力”工具。

JavaScript 内存工具类似于适用于其他应用类型的内存使用量工具。 你可以使用此工具来了解内存使用量并查找应用中的内存泄露。 有关工具的详细信息，请参阅 [JavaScript 内存](../profiling/javascript-memory.md)。

![JavaScript 内存分析工具](../profiling/media/diagjsmemory.png "DiagJSMemory")

若要对 UWP 应用执行 UI 响应能力、长时间加载和缓慢视觉对象更新诊断，请使用“HTML UI 响应能力”工具。 使用情况类似于适用于其他应用类型的应用程序时间线工具。 有关更多信息，请参阅 [HTML UI 响应能力](../profiling/html-ui-responsiveness.md)。

![HTML UI 响应能力分析工具](../profiling/media/diaghtmlresp.png "DiagHTMLResp")
::: moniker-end

::: moniker range="vs-2017"
## <a name="analyze-network-usage-uwp"></a>分析网络使用情况 (UWP)

在 UWP 应用中，你可以使用 `Windows.Web.Http` API 分析执行的网络操作。本工具可帮助你解决如访问和身份验证问题、缓存误用以及显示和下载性能差等问题。 若要使用该工具，请在性能探查器中选择“网络”，然后选择“开始”。 在应用中，浏览使用 `Windows.Web.Http` 的应用场景，然后选择“停止收集”生成报表。

![网络使用情况分析工具](../profiling/media/prof-tour-network-usage.png "诊断网络使用情况")

在摘要视图中选择一个操作，查看更多详细信息。

![网络使用情况工具中的详细信息](../profiling/media/prof-tour-network-usage-details.png "诊断网络使用情况详细信息")

有关详细信息，请参阅[网络使用情况](../profiling/network-usage.md)。
::: moniker-end

## <a name="analyze-performance-legacy-tools"></a>分析性能（旧工具）

::: moniker range="vs-2017"
如果你需要 CPU 使用率或内存使用量工具中当前不存在的功能（如检测），当你在运行桌面或 ASP.NET 应用时，可使用性能资源管理器进行分析。 （UWP 应用中不支持）。 有关详细信息，请参阅[性能资源管理器](../profiling/performance-explorer.md)。
::: moniker-end

::: moniker range=">=vs-2019"
在 Visual Studio 2019 中，旧的性能资源管理器和相关分析工具（如性能向导）已折叠到性能探查器中，可以使用“调试” > “性能探查器”来打开它们 。 在性能探查器中，可用的诊断工具取决于所选目标和当前打开的启动项目。 CPU 使用情况工具提供先前在性能向导中支持的采样功能。 检测工具提供性能向导中的检测分析功能（用于精确调用计数和持续时间）。 其他内存工具也将出现在性能探查器中。
::: moniker-end

![性能资源管理器工具](../profiling/media/prof-tour-performance-explorer.png "性能资源管理器")

## <a name="which-tool-should-i-use"></a>应使用哪一种工具？

下表列出了 Visual Studio 提供的不同工具以及适用的不同项目类型：

::: moniker range=">=vs-2019"
|性能工具|Windows 桌面|UWP|ASP.NET/ASP.NET Core|
|----------------------|---------------------|-------------|-------------|
|[性能提示](../profiling/perftips.md)|是|是|是|
|[CPU 使用率](../profiling/cpu-usage.md)|是|是|是|
|[内存使用率](../profiling/memory-usage.md)|是|是|是|
|[.NET 对象分配](../profiling/dotnet-alloc-tool.md)|是（仅用于 .NET）|是|是|
|[GPU 使用情况](/visualstudio/debugger/graphics/gpu-usage)|是|是|否|
|[应用程序时间线](../profiling/application-timeline.md)|是|是|否|
|[事件查看器](../profiling/perftips.md)|是|是|是|
|[.NET Async](../profiling/perftips.md)|是（仅用于 .NET）|是|是|
|[数据库](../profiling/perftips.md)|是（仅限 .NET Core）|否|是（仅限 ASP.NET Core）|
|[性能资源管理器](../profiling/performance-explorer.md)|否|否|否|
|[IntelliTrace](../debugger/intellitrace.md)|仅适用于带有 Visual Studio Enterprise 的 .NET|仅适用于带有 Visual Studio Enterprise 的 .NET|仅适用于带有 Visual Studio Enterprise 的 .NET|
::: moniker-end

::: moniker range="vs-2017"
|性能工具|Windows 桌面|UWP|ASP.NET/ASP.NET Core|
|----------------------|---------------------|-------------|-------------|
|[CPU 使用率](../profiling/cpu-usage.md)|是|是|是|
|[内存使用率](../profiling/memory-usage.md)|是|是|是|
|[GPU 使用情况](/visualstudio/debugger/graphics/gpu-usage)|是|是|否|
|[应用程序时间线](../profiling/application-timeline.md)|是|是|否|
|[性能提示](../profiling/perftips.md)|是|XAML 适用，HTML 不适用|是|
|[性能资源管理器](../profiling/performance-explorer.md)|是|否|是|
|[IntelliTrace](../debugger/intellitrace.md)|仅适用于带有 Visual Studio Enterprise 的 .NET|仅适用于带有 Visual Studio Enterprise 的 .NET|仅适用于带有 Visual Studio Enterprise 的 .NET|
|[网络使用情况](../profiling/network-usage.md)|否|是|否|
|[HTML UI responsiveness](../profiling/html-ui-responsiveness.md)|否|HTML 适用，XAML 不适用|否|
|[JavaScript 内存](../profiling/javascript-memory.md)|否|HTML 适用，XAML 不适用|否|
::: moniker-end


## <a name="see-also"></a>请参阅
- [在 Visual Studio 中进行调试](../debugger/debugger-feature-tour.md)
