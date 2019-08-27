---
title: 探查器命令行：检测本机组件，获取计时数据
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 36883074-9be8-4e90-a66f-7e87f21fcd30
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 605bd9e6e28f7c62ecc7a0f4a363fbbc25b58f1b
ms.sourcegitcommit: 91c7f1b525e0c22d938bc4080ba4ceac2483474f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2019
ms.locfileid: "67031967"
---
# <a name="how-to-instrument-a-native-stand-alone-component-and-collect-timing-data-with-the-profiler-from-the-command-line"></a>如何：使用探查器命令行检测本机独立组件，并收集计时数据
本主题介绍如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具检测 C++、.exe 或 .dll 文件等本机组件并收集详细的计时数据   。

> [!NOTE]
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

要使用检测方法从组件收集详细计时数据，可使用 [VSInstr.exe](../profiling/vsinstr.md) 工具生成该组件的受检测版本。 然后启动探查器。 在执行受检测组件时，会自动将计时数据收集到数据文件中。 在分析会话过程中可以暂停和恢复数据收集。

 要结束分析会话，请关闭目标应用程序，然后显式关闭探查器。

## <a name="start-the-profiling-session"></a>启动分析会话

#### <a name="to-start-profiling-by-using-the-instrumentation-method"></a>使用检测方法启动分析

1. 打开一个命令提示符窗口。

2. 使用 **VSInstr** 工具生成目标应用程序的受检测版本。

3. 启动探查器。 类型：

    **VSPerfCmd /start:trace /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) **:trace** 选项初始化探查器。

   - [/output](../profiling/output.md) **:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置。

     可以将以下一个或多个选项与 /start:trace  选项一起使用。

   | 选项 | 说明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | 指定拥有所分析进程的帐户的域和用户名。 仅当运行进程的用户不是已登录用户时，才需要此选项。 进程所有者在 Windows 任务管理器的“进程”选项卡上的“用户名”列中列出   。 |
   | [/crosssession](../profiling/crosssession.md) | 启用其他会话中的进程分析。 如果应用程序在其他会话中运行，则需要此选项。 会话标识符位于 Windows 任务管理器的“进程”选项卡上的“会话 ID”列中  。 可以将 **/CS** 指定为 **/crosssession** 的缩写。 |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | 在暂停数据收集的情况下启动探查器。 使用 [/globalon](../profiling/globalon-and-globaloff.md) 可恢复分析。 |
   | [/counter](../profiling/counter.md) **:** `Config` | 从 `Config` 中所指定的处理器性能计数器收集信息。 计数器信息将添加到在每个分析事件中收集的数据中。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | 指定要在分析期间收集的 Windows 性能计数器。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | 指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中  。 |

4. 以典型方式启动目标应用程序。

## <a name="control-data-collection"></a>控制数据收集
 在目标应用程序运行时，可以通过使用 *VSPerfCmd.exe* 选项开始和停止向文件写入数据，从而控制数据收集。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 以下选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|说明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|启动 ( **/threadon**) 或停止 ( **/threadoff**) 由线程 ID (`TID`) 指定的线程的数据收集。|

## <a name="end-the-profiling-session"></a>结束分析会话
 若要结束分析会话，请关闭正在运行受检测组件的应用程序，然后调用 **VSPerfCmd** [/shutdown](../profiling/shutdown.md) 选项来关闭探查器和分析数据文件。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 关闭目标应用程序。

2. 关闭探查器。 类型：

     **VSPerfCmd /shutdown**

## <a name="see-also"></a>请参阅
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [检测方法数据视图](../profiling/instrumentation-method-data-views.md)