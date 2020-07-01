---
title: 将探查器附加到 .NET 应用以收集内存数据
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: dbe8f0cdb976dfb687071b231b2907b6b7124b3a
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2020
ms.locfileid: "85328736"
---
# <a name="how-to-attach-the-profiler-to-a-net-framework-stand-alone-application-to-collect-memory-data-by-using-the-command-line"></a>如何：将探查器附加到 .NET Framework 独立应用程序，以使用命令行收集内存数据

本文介绍如何使用 Visual Studio 分析工具命令行工具将探查器附加到正在运行的 .NET Framework 独立（客户端）应用程序，并收集内存数据。

> [!NOTE]
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

若要附加到 .NET Framework 应用程序并收集内存数据，必须使用 [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) 工具初始化相应的环境变量，然后才能启动目标应用程序。 将探查器附加到应用程序时，可以使用 *VSPerfCmd.exe* 工具暂停和继续数据收集。

若要结束分析会话，必须将探查器与所有被分析进程分离，并且必须显式关闭探查器。 在大多数情况下，建议在会话结束时清除分析环境变量。

## <a name="attach-the-profiler"></a>附加探查器

### <a name="to-attach-the-profiler-to-a-running-net-framework-application"></a>将探查器附加到正在运行的 .NET Framework 应用程序

1. 打开一个命令提示符窗口。

2. 初始化分析环境变量。 类型：

     **VSPerfClrEnv** { **/samplegc** &#124; **/samplegclife**} [ **/samplelineoff**]

    - /samplegc  和 /samplegclife  选项指定是仅收集内存分配数据，还是同时收集内存分配数据和对象生存期数据。 必须指定一个且仅指定一个选项。

        |选项|说明|
        |------------|------------------|
        |**/samplegc**|仅收集内存分配数据。|
        |**/samplegclife**|同时收集内存分配数据和对象生存期数据。|

    - /samplelineoff  选项禁用源代码行号数据的收集。

3. 启动探查器。 类型：

     **VSPerfCmd /start:sample /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) **:sample** 选项初始化探查器。

   - [/output](../profiling/output.md) **:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置。

     可以将以下任意选项与 **/start:sample** 选项一起使用。

     | 选项 | 描述 |
     | - | - |
     | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | 指定拥有所分析进程的帐户的域和用户名。 仅当运行进程的用户不是已登录用户时，才需要此选项。 进程所有者在 Windows 任务管理器的“进程”选项卡上的“用户名”列中列出。 |
     | [/crosssession &#124; /cs](../profiling/crosssession.md) | 启用其他会话中的进程分析。 如果应用程序在其他会话中运行，则需要此选项。 会话标识符在 Windows 任务管理器的“进程”选项卡上的“会话 ID”列中列出。 可以将 **/CS** 指定为 **/crosssession** 的缩写。 |
     | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | 指定要在分析期间收集的 Windows 性能计数器。 |
     | [/automark](../profiling/automark.md) **:** `Interval` | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。 |

4. 如有必要，通过典型方式启动目标应用程序。

5. 将探查器附加到目标应用程序。 类型：

     **VSPerfCmd**  [/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [[/targetclr](../profiling/targetclr.md) **:** `Version`]

    - `PID` 指定目标应用程序的进程 ID。 `ProcessName` 指定进程的名称。 请注意，如果指定 `ProcessName` 且运行具有相同名称的多个进程，则结果不可预测。 可以在 Windows 任务管理器中查看所有运行中的进程的进程 ID。

    - /targetclr: `Version` 指定应用程序中加载运行时的多个版本时要分析的公共语言运行时 (CLR) 的版本  。 可选。

## <a name="control-data-collection"></a>控制数据收集

在目标应用程序运行时，可以通过使用 *VSPerfCmd.exe* 选项开始和停止向文件写入数据，从而控制数据收集。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 以下选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|描述|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|对由 `PID` 指定的进程，启动 (/processon  ) 或停止 (/processoff  ) 数据收集。|
    |[/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[ **:** {`PID`&#124;`ProcName`}]|/attach  将启动由 `PID` 或进程名称 (ProcName) 指定的进程的数据收集。 **/detach** 将停止指定进程或所有进程（未指定任何特定进程时）的数据收集。|

## <a name="end-the-profiling-session"></a>结束分析会话

若要结束分析会话，必须将探查器与所有被分析进程分离，并且必须显式关闭探查器。 可通过关闭应用程序或调用 **VSPerfCmd /detach** 选项从使用采样方法分析的应用程序分离探查器。 然后，可以调用 **VSPerfCmd /shutdown** 选项关闭探查器和分析数据文件。 **VSPerfClrEnv /off** 命令会清除分析环境变量。

### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 执行下列步骤之一，从目标应用程序分离探查器：

    - 键入 **VSPerfCmd /detach**

         \- 或 -

    - 关闭目标应用程序。

2. 关闭探查器。 类型：

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)

3. （可选）清除分析环境变量。 类型：

     **VSPerfCmd /off**

## <a name="see-also"></a>请参阅

[配置文件独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
[.NET 内存数据视图](../profiling/dotnet-memory-data-views.md)
