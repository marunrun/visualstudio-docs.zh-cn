---
title: 探查器命令行：检测 .NET 服务，获取计时详细信息
ms.date: 11/04/2016
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 4f3e03a35719e6dd1cbfa7514a304539dc4f0ca1
ms.sourcegitcommit: 91c7f1b525e0c22d938bc4080ba4ceac2483474f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2019
ms.locfileid: "67032056"
---
# <a name="how-to-instrument-a-net-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line"></a>如何：使用探查器命令行检测 .NET 服务，并收集详细计时数据

本文介绍如何使用 Visual Studio 分析工具命令行工具检测 .NET Framework 服务和收集详细计时数据。

> [!NOTE]
> 如果某服务在计算机启动之后无法重启（此类服务只能在操作系统启动时启动），则无法使用检测方法分析该服务。
>
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。
>
> 若要将层交互数据添加到分析运行，需要使用命令行分析工具执行特定的步骤。 请参阅[收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md)。

要使用检测方法从 .NET Framework 服务收集详细计时数据，可使用 [VSInstr.exe](../profiling/vsinstr.md) 工具生成该组件的检测版本。 然后，将该服务的非检测版本替换为检测版本，确保将该服务配置为手动启动。 使用 [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) 工具初始化全局分析环境变量，然后重启主计算机。 然后启动探查器。

启动该服务时，会自动将计时数据收集到数据文件中。 在分析会话过程中可以暂停和恢复数据收集。

若要结束分析会话，可关闭该服务，然后显式关闭探查器。 在大多数情况下，建议在会话结束时清除分析环境变量。

## <a name="start-the-application-with-the-profiler"></a>用探查器启动应用程序

1. 打开命令提示符窗口。

2. 使用 VSInstr  工具生成该服务二进制文件的检测版本。

3. 使用检测版本替换原始二进制文件。 在 Windows 服务控制管理器中，确保将该服务的“启动类型”设置为“手动”。

4. 初始化 .NET Framework 分析环境变量。 类型：

     **VSPerfClrEnv /globaltraceon**

5. 重新启动计算机。

6. 打开命令提示符窗口。

7. 启动探查器。 类型：

     **VSPerfCmd /start:trace /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) **:trace** 选项初始化探查器。

   - [/output](../profiling/output.md) **:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置  。

     可以将以下任一选项与 /start:trace  选项一起使用。

     > [!NOTE]
     > /User  和 /crosssession  选项通常为分析服务所需选项。

     | 选项 | 说明 |
     | - | - |
     | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | 指定拥有所分析进程的帐户的域和用户名。 仅在进程以已登录用户外的用户身份运行时才需要此选项。 进程所有者在 Windows 任务管理器的“进程”选项卡上的“用户名”列中列出   。 |
     | [/crosssession](../profiling/crosssession.md) | 启用其他会话中的进程分析。 如果应用程序在其他会话中运行，则需要此选项。 会话 ID 位于 Windows 任务管理器的“进程”选项卡上的“会话 ID”列中   。 可以将 **/CS** 指定为 **/crosssession** 的缩写。 |
     | [/waitstart](../profiling/waitstart.md)[ **:** `Interval`] | 指定探查器返回错误前，等待探查器初始化的秒数。 如果未指定 `Interval`，则探查器将无限期等待。 默认情况下，  /start 将立即返回。 |
     | [/globaloff](../profiling/globalon-and-globaloff.md) | 若要启动探查器而暂停数据收集，请将 **/globaloff** 选项添加到 **/start** 命令行。 使用 **/globalon** 可恢复分析。 |
     | [/counter](../profiling/counter.md) **:** `Config` | 从 Config 中所指定的处理器性能计数器收集信息。计数器信息将添加到在每个分析事件中收集的数据中。 |
     | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | 指定要在分析期间收集的 Windows 性能计数器。 |
     | [/automark](../profiling/automark.md) **:** `Interval` | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。 |
     | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | 指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中  。 |

8. 从 Windows 服务控制管理器启动服务。

## <a name="control-data-collection"></a>控制数据收集

服务运行时，可使用 VSPerfCmd.exe  选项开始或停止将数据写入到探查器数据文件。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭服务）进行数据收集。

- 以下 **VSPerfCmd** 选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|说明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|启动 ( **/threadon**) 或停止 ( **/threadoff**) 由线程 ID (`TID`) 指定的线程的数据收集。|

## <a name="end-the-profiling-session"></a>结束分析会话

若要结束分析会话，请停止正在运行受检测组件的服务，然后调用 VSPerfCmd  [/shutdown](../profiling/shutdown.md) 选项来关闭探查器和分析数据文件。 VSPerfClrEnv /globaloff 命令会清除分析环境变量  。

必须重启计算机才能应用新的环境设置。

1. 从服务控制管理器停止服务。

2. 关闭探查器。 类型：

     **VSPerfCmd /shutdown**

3. 完成所有分析后，清除分析环境变量。 类型：

     VSPerfClrEnv /globaloff 

4. 使用原始模块替换被检测模块。 如有必要，重新配置服务的“启动类型”。

5. 重新启动计算机。

## <a name="see-also"></a>请参阅

[配置文件服务](../profiling/command-line-profiling-of-services.md)
[检测方法数据视图](../profiling/instrumentation-method-data-views.md)
