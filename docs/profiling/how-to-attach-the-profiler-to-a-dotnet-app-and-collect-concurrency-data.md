---
title: 将探查器附加到 .NET 应用以收集并发数据 | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: fdd41576-797e-4312-8520-fee7bb767e4a
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: f44213bf7356d499f852b53335698c701bf03eb7
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74779150"
---
# <a name="how-to-attach-the-profiler-to-a-net-framework-stand-alone-application-to-collect-concurrency-data-by-using-the-command-line"></a>如何：将探查器附加到 .NET Framework 独立应用程序，以使用命令行收集并发数据
本文介绍如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具将探查器附加到正在运行的 .NET Framework 独立（客户端）应用程序，并收集进程和线程并发数据。

> [!NOTE]
> 若要获取分析工具的路径，请参阅[演练：使用探查器 API](../profiling/walkthrough-using-profiler-apis.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。 有关详细信息，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。

 将探查器附加到应用程序时，可以暂停和恢复数据收集。 若要结束分析会话，探查器不得再附加于应用程序，并且必须显式关闭探查器。

## <a name="attach-the-profiler"></a>附加探查器

#### <a name="to-attach-the-profiler-to-a-running-net-framework-application"></a>将探查器附加到正在运行的 .NET Framework 应用程序

1. 打开命令提示符窗口。

2. 启动探查器。 类型：

     [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency  /output:** `OutputFile` [`Options`]

     [/output](../profiling/output.md) **:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置。

     可以将以下任意选项与 **/start:concurrency** 选项一起使用。

    |选项|说明|
    |------------|-----------------|
    |[/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`|指定要在分析期间收集的 Windows 性能计数器。|
    |[/automark](../profiling/automark.md) **:** `Interval`|仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。|
    |[/events](../profiling/events-vsperfcmd.md) **:** `Config`|指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中。|

3. 以典型方式启动目标应用程序。

4. 将探查器附加到目标应用程序。 类型：

     **VSPerfCmd /attach:** `PID` [ **/lineoff**] [ **/targetclr:** `Version`]

    - `PID` 指定目标应用程序的进程 ID。 可以在 Windows 任务管理器中查看所有运行中的进程的进程 ID。

    - [/lineoff](../profiling/lineoff.md) 将禁用行号数据的收集。

    - [/targetclr](../profiling/targetclr.md) **:** `Version` 指定应用程序中加载运行时的多个版本时要分析的公共语言运行时 (CLR) 的版本。 可选。

## <a name="control-data-collection"></a>控制数据收集
 在目标应用程序运行时，可以通过使用 *VSPerfCmd.exe* 选项开始和停止向文件写入数据，从而控制数据收集。 通过控制数据收集，使你能够针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 以下 VSPerfCmd.exe 选项对可启动和停止数据收集  。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|说明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|
    |[/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[ **:** {`PID`&#124;`ProcName`}]|**/attach** 将启动由进程 ID (`PID`) 或进程名称 (ProcName) 指定的进程的数据收集。 **/detach** 将停止指定进程或所有进程（未指定任何特定进程时）的数据收集。|

## <a name="end-the-profiling-session"></a>结束分析会话
 若要结束分析会话，探查器不得再收集数据。 可通过关闭应用程序或调用 **VSPerfCmd /detach** 选项从使用并发方法分析的应用程序停止数据收集。 然后，可以调用 **VSPerfCmd /shutdown** 选项关闭探查器和分析数据文件。 **VSPerfClrEnv /off** 命令会清除分析环境变量。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 执行下列操作之一以从目标应用程序中分离探查器。

    - 键入 **VSPerfCmd /detach**

         -或-

    - 关闭目标应用程序。

2. 关闭探查器。 类型：

     VSPerfCmd[/shutdown](../profiling/shutdown.md)
