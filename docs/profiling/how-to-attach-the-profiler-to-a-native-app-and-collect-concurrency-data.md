---
title: 将探查器附加到本机应用程序中并收集并发数据
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 12d3e0f3-4b74-4e66-8fbf-8ac99bd4f91c
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- cplusplus
ms.openlocfilehash: dcc125f795a29f53abb07920aa11c9a5e6ee966b
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329525"
---
# <a name="how-to-attach-the-profiler-to-a-native-stand-alone-application-and-collect-concurrency-data-by-using-the-command-line"></a>如何：将探查器附加到本机独立应用程序，并使用命令行收集并发数据
本文介绍如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具将探查器附加到运行中的本机 (C/C++) 独立应用程序并收集线程争用数据。

> [!NOTE]
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

 将探查器附加到应用程序时，可以暂停和恢复数据收集。 若要结束分析会话，探查器不得再附加于应用程序，并且必须显示关闭探查器。

## <a name="attach-the-profiler-to-a-running-native-application"></a>将探查器附加到正在运行的本机应用程序

#### <a name="to-attach-the-profiler-to-a-running-native-application"></a>将探查器附加到正在运行的本机应用程序

1. 在命令提示符下，键入以下命令：

     [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency**

     可以将下表中的任意选项与 **/start:concurrency** 选项一起使用。

    |选项|描述|
    |------------|-----------------|
    |[/user](../profiling/user-vsperfcmd.md) **:** [`Domain\`]`Username`|指定要向探查器授予访问权限的帐户的可选域和用户名。|
    |[/crosssession](../profiling/crosssession.md)|启用其他登录会话中的进程分析。|
    |[/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`|指定要在分析期间收集的 Windows 性能计数器。|
    |[/automark](../profiling/automark.md) **:** `Interval`|仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500。|
    |[/events](../profiling/events-vsperfcmd.md) **:** `Config`|指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中。|

2. 在命令提示符下输入以下命令以将探查器附加到目标应用程序：

     **VSPerfCmd**  [/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`}

     `PID` 指定目标应用程序的进程 ID。 可以在 Windows 任务管理器中查看所有运行中的进程的进程 ID。

## <a name="control-data-collection"></a>控制数据收集
 在目标应用程序运行时，可以通过使用 *VSPerfCmd.exe* 选项开始和停止向文件写入数据，从而控制数据收集。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 下表中的选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|描述|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|
    |[/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[ **:** {`PID`&#124;`ProcName`}]|**/attach** 将启动由进程 ID (`PID`) 或进程名称 (*ProcName*) 指定的进程的数据收集。 **/detach** 将停止指定进程或所有进程（未指定任何特定进程时）的数据收集。|

## <a name="end-the-profiling-session"></a>结束分析会话
 若要结束分析会话，探查器不得再收集数据。 可通过关闭应用程序或调用 **VSPerfCmd /detach** 选项从使用采样方法分析的应用程序停止数据收集。 然后，可以调用 **VSPerfCmd /shutdown** 选项关闭探查器和分析数据文件。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 通过将其关闭或键入以下命令将探查器与目标应用程序分离：

     **VSPerfCmd /detach**

2. 通过键入以下命令关闭探查器：

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)
