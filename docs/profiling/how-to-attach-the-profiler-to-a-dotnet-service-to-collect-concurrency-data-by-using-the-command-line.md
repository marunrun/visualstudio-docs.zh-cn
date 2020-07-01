---
title: 将探查器附加到 .NET 服务以收集并发数据
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: ffbdfe37-8325-44be-bd36-2c8aab2dec7b
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 24c49015915b8a1d214a833c38c5550f51c50c13
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2020
ms.locfileid: "85328691"
---
# <a name="how-to-attach-the-profiler-to-a-net-service-to-collect-concurrency-data-by-using-the-command-line"></a>如何：将探查器附加到 .NET 服务，以使用命令行收集并发数据
本文介绍如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具将探查器附加到 .NET Framework 服务，并使用采样方法收集进程和线程并发数据。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

> [!NOTE]
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

 若要收集并发数据，请将探查器附加到服务进程。 将探查器附加到服务时，可以暂停和恢复数据收集。 若要结束分析会话，探查器不得再附加于服务，且须显示关闭探查器。 在大多数情况下，建议在会话结束时清除分析环境变量。

## <a name="attach-the-profiler"></a>附加探查器

#### <a name="to-attach-the-profiler-to-a-net-framework-service"></a>将探查器附加到 .NET Framework 服务

1. 安装服务。

2. 打开命令窗口。

3. 初始化分析环境变量。 类型：

     [VSPerfClrEnv](../profiling/vsperfclrenv.md) **/globalsampleon** [ **/samplelineoff**]

    - **/globalsampleon** 启用采样。

    - **/samplelineoff** 禁用向特定源代码行分配收集的数据。 指定此选项时，仅向函数分配数据。

4. 重新启动计算机。

5. 启动探查器。 类型：

     [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency  /output:** `OutputFile` [`Options`]

     [/output](../profiling/output.md) **:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置。

     可将下表中的任意选项与 **/start** 选项一起使用。

    > [!NOTE]
    > **/User** 和 **/crosssession** 选项通常为服务所需选项。

    |选项|描述|
    |------------|-----------------|
    |[/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName`|指定拥有所分析进程的帐户的域和用户名。 仅在进程以已登录用户外的用户身份运行时才需要此选项。 进程所有者在 Windows 任务管理器的“进程”选项卡上的“用户名”列中列出   。|
    |[/crosssession](../profiling/crosssession.md)|启用其他会话中的进程分析。 在其他的会话中运行该服务时需要此选项。 会话 ID 位于 Windows 任务管理器的“进程”选项卡上的“会话 ID”列中   。 可以将 **/CS** 指定为 **/crosssession** 的缩写。|
    |[/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`|指定要在分析期间收集的 Windows 性能计数器。|
    |[/automark](../profiling/automark.md) **:** `Interval`|仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。|
    |[/events](../profiling/events-vsperfcmd.md) **:** `Config`|指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中  。|

6. 必要时，请启动该服务。

7. 将探查器附加到该服务。 类型：

     **VSPerfCmd /attach:** `PID` [[/targetclr](../profiling/targetclr.md) **:** `Version`]

    - `PID` 指定服务的进程 ID 或进程名称。 可以在 Windows 任务管理器中查看所有运行中的进程的进程 ID。

    - targetclr: `Version` 指定应用程序中加载运行时的多个版本时要分析的公共语言运行时 (CLR) 的版本  。 可选。

## <a name="control-data-collection"></a>控制数据收集
 服务运行时，使用通过使用 VSPerfCmd.exe 选项开始和停止向文件的数据写入，从而控制数据收集  。 通过控制数据收集，使你能够针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 以下 **VSPerfCmd** 选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|描述|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|
    |**/attach:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[:{`PID`&#124;`ProcName`}]|**/attach** 将启动由进程 ID 或进程名称指定的进程的数据收集。 **/detach** 将停止指定进程或所有进程（未指定任何特定进程时）的数据收集。|

- 还可以使用 **VSPerfCmd.exe**[/mark](../profiling/mark.md) 选项将分析标记插入数据文件。 **/mark**命令可添加标识符、时间戳和（可选）用户定义的文本字符串。 标记可用于筛选探查器报告和数据视图中的数据。 以下 VSPerfCmd 选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

## <a name="end-the-profiling-session"></a>结束分析会话
 若要结束分析会话，探查器不得再收集数据。 可通过停止服务或调用 **VSPerfCmd /detach** 选项从使用并发方法分析的应用程序停止数据收集。 然后，可以调用 **VSPerfCmd /shutdown** 选项关闭探查器和分析数据文件。 **VSPerfClrEnv /globaloff** 命令可清除分析环境变量，但在重新启动计算机前不会重置系统配置。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 执行下列操作之一以从目标应用程序中分离探查器。

    - 停止服务。

         \- 或 -

    - 键入 **VSPerfCmd /detach.**

2. 关闭探查器。 类型：

     **VSPerfCmd**  [Shutdown](../profiling/shutdown.md)
