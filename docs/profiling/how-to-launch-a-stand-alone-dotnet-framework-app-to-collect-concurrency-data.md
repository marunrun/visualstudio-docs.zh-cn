---
title: 探查器命令行：打开客户端 .NET 应用，获取并发数据
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 17a48848-bd3e-44ef-9971-e39836ff1df2
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 4a52c65f8a53d62edde42c26fafef9940046ba5d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74775387"
---
# <a name="how-to-launch-a-stand-alone-net-framework-application-with-the-profiler-to-collect-concurrency-data-by-using-the-command-line"></a>如何：使用探查器启动独立 .NET Framework 应用程序，并通过命令行收集并发数据
本主题介绍了如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具启动 .NET Framework 独立（客户端）应用程序，并收集进程和线程并发数据

> [!NOTE]
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

 将探查器附加到应用程序时，可以暂停和恢复数据收集。 若要结束分析会话，探查器不得再附加于应用程序，并且必须显示关闭探查器。

## <a name="start-the-application-with-the-profiler"></a>用探查器启动应用程序
 要使用探查器启动 .NET Framework 目标应用程序，请使用 VSPerfClrEnv.exe 设置 .NET Framework 分析变量  。 然后，使用 VSPerfCmd /start  和 /launch  选项，以初始化探查器并启动应用程序。 可以在单个命令行中指定 **/start** 和 **/launch** 及其各自的选项。 还可以向命令行添加 /globaloff  选项，以在目标应用程序启动时暂停数据收集。 然后，对单独命令行使用 /globalon  ，以开始收集数据。

#### <a name="to-start-an-application-with-the-profiler"></a>用探查器启动应用程序

1. 打开命令提示符窗口。

2. 启动探查器。 类型：

    [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency**[ **,** {**ResourceOnly**&#124;**ThreadOnly**}] **/output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) 选项可初始化探查器。

     | | |
     |-------------------------------------| - |
     | **/start:concurrency** | 允许收集资源争用和线程执行数据。 |
     | **/start:concurrency,resourceonly** | 允许仅收集资源争用数据。 |
     | **/start:concurrency,threadonly** | 允许仅收集线程执行数据。 |

   - [/output](../profiling/output.md) **:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置。

     可以将以下任意选项与 **/start:concurrency** 选项一起使用。

   | 选项 | 描述 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`domain\`]`username` | 指定要向探查器授予访问权限的帐户的可选域和用户名。 |
   | [/crosssession](../profiling/crosssession.md) | 启用其他登录会话中的进程分析。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | 指定要在分析期间收集的 Windows 性能计数器。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | 指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中  。 |

3. 启动目标应用程序。 类型：

    **VSPerfCmd**  [/launch](../profiling/launch.md) **:** `AppName` [`Options`] [`Sample Event`]

    可以将以下任意选项与 **/launch** 选项一起使用。

   |选项|描述|
   |------------|-----------------|
   |[/args](../profiling/args.md) **:** `Arguments`|指定一个字符串，其中包含要传递给目标应用程序的命令行参数。|
   |[/console](../profiling/console.md)|在另一个窗口中启动目标命令行应用程序。|
   |[/targetclr](../profiling/targetclr.md) **:** `Version`|指定应用程序中加载公共语言运行时 (CLR) 的多个版本时要分析的运行时的版本。|

## <a name="control-data-collection"></a>控制数据收集
 在目标应用程序运行时，可以通过使用 *VSPerfCmd.exe* 选项开始和停止向文件写入数据，从而控制数据收集。 通过控制数据收集，使你能够针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

1. 以下 VSPerfCmd.exe 选项对可启动和停止数据收集  。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|描述|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|
    |[/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[ **:** {`PID`&#124;`ProcName`}]|**/attach** 将启动由进程 ID (`PID`) 或进程名称 (ProcName) 指定的进程的数据收集。 **/detach** 将停止指定进程或所有进程（未指定任何特定进程时）的数据收集。|

## <a name="end-the-profiling-session"></a>结束分析会话
 若要结束分析会话，探查器不得再收集数据。 可以通过关闭所分析的应用程序或调用 **VSPerfCmd /detach** 选项来停止收集并发数据。 然后，可以调用 **VSPerfCmd /shutdown** 选项关闭探查器和分析数据文件。 **VSPerfClrEnv /off** 命令会清除分析环境变量。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 执行下列操作之一以从目标应用程序中分离探查器。

    - 关闭目标应用程序。

         \- 或 -

    - 键入 **VSPerfCmd /detach**

2. 关闭探查器

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)

## <a name="see-also"></a>请参阅
- [收集并发数据](../profiling/collecting-concurrency-data-for-stand-alone-applications.md)
