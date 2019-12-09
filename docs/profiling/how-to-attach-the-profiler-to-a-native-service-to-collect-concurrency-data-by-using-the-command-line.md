---
title: VSPerfCmd：将探查器附加到本机服务以获取并发数据
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 283a1ee1-b43e-4daf-95ae-1311925a42a8
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- cplusplus
ms.openlocfilehash: 705e55363f4f8657da20fe66cd4369188f133cdb
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74776603"
---
# <a name="how-to-attach-the-profiler-to-a-native-service-to-collect-concurrency-data-by-using-the-command-line"></a>如何：将探查器附加到本机服务，以使用命令行收集并发数据
本文介绍如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具将探查器附加到本机 (C/C++) 服务并使用采样方法收集进程和线程并发数据。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

> [!NOTE]
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

 将探查器附加到服务时，可以暂停和恢复数据收集。 若要结束分析会话，探查器不得再附加于服务，且须显示关闭探查器。

## <a name="attach-the-profiler"></a>附加探查器
 若要将探查器附加到本机服务，请使用 **VSPerfCmd/start** 和 **/attach** 选项初始化探查器，并将其附加到目标应用程序。 可以在单个命令行中指定 **/start** 和 **/attach** 及其各自的选项。 还可以添加 **/globaloff** 选项，以在目标应用程序启动时暂停数据收集。 然后可使用 **/globalon** 开始收集数据。

#### <a name="to-attach-the-profiler-to-a-native-service"></a>将探查器附加到本机服务

1. 如果服务未运行，请启动该服务。

2. 在命令提示符中键入以下内容以启动探查器：

    [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency   /output:** `OutputFile` [`Options`]

   - [/output](../profiling/output.md) **:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置。

     可将下表中的任意选项与 **/start** 选项一起使用。

   > [!NOTE]
   > 大多数服务都需要 **/user** 和 **/crosssession** 选项。

   | 选项 | 说明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain\`]`UserName` | 指定要向探查器授予访问权限的帐户的可选域和用户名。 |
   | [/crosssession](../profiling/crosssession.md) | 启用其他登录会话中的进程分析。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | 指定要在分析期间收集的 Windows 性能计数器。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | 指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中。 |

3. 在命令提示符中键入以下命令以将探查器附加到服务：

    **VSPerfCmd /attach:** `PID`

    `PID` 指定目标应用程序的进程 ID 或进程名称。 可以在 Windows 任务管理器中查看所有运行中的进程的进程 ID。

## <a name="control-data-collection"></a>控制数据收集
 目标应用程序运行时，可通过使用 VSPerfCmd.exe 选项开始和停止向文件写入数据，从而控制数据收集  。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 下表中的选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|说明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|
    |[/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[ **:** {`PID`&#124;`ProcName`}]|**/attach** 将启动由进程 ID (`PID`) 或进程名称 (*ProcName*) 指定的进程的数据收集。 **/detach** 将停止指定进程或所有进程（未指定任何特定进程时）的数据收集。|

## <a name="end-the-profiling-session"></a>结束分析会话
 若要结束分析会话，探查器不得再收集数据。 可通过停止服务或调用 **VSPerfCmd /detach** 选项从使用并发方法分析的本机服务停止数据收集。 然后，可以调用 **VSPerfCmd /shutdown** 选项关闭探查器和分析数据文件。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 通过停止服务或在命令提示符中键入以下命令将探查器与目标应用程序分离：

     键入 **VSPerfCmd /detach**

2. 在命令提示符下键入以下命令以关闭探查器：

     **VSPerfCmd** [/shutdown](../profiling/shutdown.md)
