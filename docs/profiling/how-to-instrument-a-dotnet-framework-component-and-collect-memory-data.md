---
title: 探查器命令行：检测客户端 .NET 组件，获取内存数据
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d09cc46a-70f5-48f9-aa24-89913e67b359
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 76d216c4f112f88001b0314a23f22e689f729106
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74775896"
---
# <a name="how-to-instrument-a-stand-alone-net-framework-component-and-collect-memory-data-with-the-profiler-by-using-the-command-line"></a>如何：使用探查器命令行检测独立 .NET Framework 组件，并收集内存数据
本文介绍如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具检测独立应用程序的 .NET Framework 组件（如 .exe 或 .dll 文件）以及如何使用探查器收集内存信息。

> [!NOTE]
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

 若要使用检测方法收集 .NET Framework 组件的内存数据，可使用 [VSInstr.exe](../profiling/vsinstr.md) 工具生成该组件的受检测版本，并使用 [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) 工具初始化分析环境变量。 然后使用 *VSPerfCmd.exe* 工具启动探查器。

 在执行受检测组件时，会自动将内存数据收集到数据文件中。 在分析会话过程中可以暂停和恢复数据收集。

 若要结束分析会话，请关闭目标应用程序，然后显式关闭探查器。 在大多数情况下，建议在会话结束时清除分析环境变量。

## <a name="start-the-application-with-the-profiler"></a>用探查器启动应用程序

#### <a name="to-attach-the-profiler-to-a-running-net-framework-application"></a>将探查器附加到正在运行的 .NET Framework 应用程序

1. 打开一个命令提示符窗口。

2. 使用 **VSInstr** 工具生成目标应用程序的受检测版本。

3. 初始化 .NET Framework 分析环境变量。 类型：

    **VSPerfClrEnv** { **/tracegc** &#124; **/tracegclife**}

   - **/tracegc** 和 **/tracegclife** 选项用于初始化环境变量，以便只收集内存分配数据，或同时收集内存分配数据和对象生存期数据。

       |选项|描述|
       |------------|-----------------|
       |**/tracegc**|只启用对内存分配数据的收集。|
       |**/tracegclife**|启用对内存分配数据和对象生存期数据的收集。|

4. 启动探查器。 类型：

    **VSPerfCmd /start:trace /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) **:trace** 选项初始化探查器。

   - [/output](../profiling/output.md) **:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置  。

     可以将以下任意选项与 **/start:trace** 选项一起使用。

   | 选项 | 描述 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | 指定拥有所分析进程的帐户的域和用户名。 仅当运行进程的用户不是已登录用户时，才需要此选项。 进程所有者在 Windows 任务管理器的“进程”选项卡上的“用户名”列中列出  。 |
   | [/crosssession](../profiling/crosssession.md) | 启用其他会话中的进程分析。 如果应用程序在其他会话中运行，则需要此选项。 会话标识符在 Windows 任务管理器的“进程”选项卡上的“会话 ID”列中列出   。 可以将 **/CS** 指定为 **/crosssession** 的缩写。 |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | 若要启动探查器而暂停数据收集，请将 **/globaloff** 选项添加到 **/start** 命令行。 使用 **/globalon** 可恢复分析。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | 指定要在分析期间收集的 Windows 性能计数器。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。 |
   | [/counter](../profiling/counter.md) **:** `Config` | 从 Config 中所指定的处理器性能计数器收集信息。计数器信息将添加到在每个分析事件中收集的数据中。 |
   | [events](../profiling/events-vsperfcmd.md) **:** `Config` | 指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中  。 |

5. 从命令提示符窗口中启动目标应用程序。

## <a name="control-data-collection"></a>控制数据收集
 在目标应用程序运行时，可以通过使用 *VSPerfCmd.exe* 选项开始和停止向文件写入数据，从而控制数据收集。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 以下 **VSPerfCmd** 选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|描述|
    |------------|-----------------|
    |[/globalon](../profiling/globalon-and-globaloff.md) [/globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|启动 ( **/threadon**) 或停止 ( **/threadoff**) 由线程 ID (`TID`) 指定的线程的数据收集。|

## <a name="end-the-profiling-session"></a>结束分析会话
 若要结束分析会话，请关闭正在运行受检测组件的应用程序，然后调用 VSPerfCmd [/shutdown](../profiling/shutdown.md) 选项来关闭探查器和分析数据文件  。 **VSPerfClrEnv /off** 命令会清除分析环境变量。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 关闭目标应用程序。

2. 关闭探查器。 类型：

     **VSPerfCmd /shutdown**

3. （可选）清除分析环境变量。 类型：

     **VSPerfCmd /off**

## <a name="see-also"></a>请参阅
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [.NET 内存数据视图](../profiling/dotnet-memory-data-views.md)
