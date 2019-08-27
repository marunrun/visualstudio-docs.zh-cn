---
title: 将探查器附加到 .NET Framework 独立应用程序；获取应用程序统计信息
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: b62fcbc1-791f-474e-890a-a6c332e0c9ea
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: c23fe867c3825958f1e2f1c3b7fedc3dd15d840e
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66261609"
---
# <a name="how-to-attach-the-profiler-to-a-net-framework-stand-alone-application-and-collect-application-statistics-by-using-the-command-line"></a>如何：将探查器附加到 .NET Framework 独立应用程序，并使用命令行收集应用程序统计信息
本文介绍了如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具将探查器附加到正在运行的 .NET Framework 独立（客户端）应用程序，并使用采样方法收集性能统计信息。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。
>
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。
>
> 若要将层交互数据添加到分析运行，需要使用命令行分析工具执行特定的步骤。 请参阅[收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md)。

 若要从 .NET Framework 应用程序收集性能数据，必须在目标应用程序启动前初始化相应的环境变量。 将探查器附加到应用程序时，可以暂停和恢复数据收集。

 若要结束分析会话，探查器不得再附加于应用程序，并且必须显示关闭探查器。 大多数情况下，建议在分析会话结束时清除分析环境变量。

## <a name="attach-the-profiler"></a>附加探查器

#### <a name="to-attach-the-profiler-to-a-running-net-framework-application"></a>将探查器附加到正在运行的 .NET Framework 应用程序

1. 打开一个命令提示符窗口。

2. 初始化分析环境变量。 类型：

    VSPerfClrEnv /sampleon [/samplelineoff]

   - /samplelineoff 选项禁用源代码行号数据的收集。

3. 启动探查器。 类型：

    **VSPerfCmd /start:sample /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md)**:sample** 选项初始化探查器。

   - [/output](../profiling/output.md)**:**`OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置。

     可以将以下任意选项与 /start:sample 选项一起使用。

   | 选项 | 说明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` | 指定拥有分析进程的帐户的可选域和用户名。 仅当以用户身份（而不是已登录用户身份）启动分析应用程序时，才需要使用此选项。 |
   | [/crosssession](../profiling/crosssession.md) | 启用其他登录会话中的进程分析。 可以将 **/CS** 指定为 **/crosssession** 的缩写。 如果应用程序在其他会话中运行，则需要此选项。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | 指定要在分析期间收集的 Windows 性能计数器。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | 指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中。 |

4. 如有必要，通过典型方式启动目标应用程序。

5. 将探查器附加到目标应用程序。 类型：

    VSPerfCmd /attach:{`PID`&#124;`ProcessName`} [`Sample Event`] [/targetclr:`Version`]

   - `PID` 指定目标应用程序的进程 ID。 `ProcessName` 指定进程的名称。 请注意，如果指定 `ProcessName` 且运行具有相同名称的多个进程，则结果不可预测。 可以在 Windows 任务管理器中查看所有运行中的进程的进程 ID。

   - [/targetclr](../profiling/targetclr.md) **:** `Version` 指定应用程序中加载运行时的多个版本时要分析的公共语言运行时 (CLR) 的版本。 可选。

   - 默认情况下，性能数据为每 10,000,000 个非暂停处理器时钟周期采样一次。 在 1GH 的处理器上，大约每 10 秒一次。 可以指定下面的选项之一，更改时钟周期间隔或指定其他采样事件。[/targetclr](../profiling/targetclr.md):`Version` 指定应用程序中加载运行时的多个版本时要分析的 CLR 版本。 可选。

   |||
   |-|-|
   |样本事件|说明|
   |[/timer](../profiling/timer.md) **:** `Interval`|将采样间隔更改为 `Interval` 所指定的非暂停时钟周期数目。|
   |[/pf](../profiling/pf.md) [:`Interval`]|将采样事件更改为页面错误。 如果已指定 `Interval`，则会设置样本之间的页面错误数目。 默认值为 10。|
   |[/sys](../profiling/sys-vsperfcmd.md) [**:**`Interval`]|将采样事件更改为从进程对操作系统内核的系统调用 (syscall)。 如果已指定 `Interval`，则会设置样本之间的调用次数。 默认值为 10。|
   |[/counter](../profiling/counter.md) **:** `Config`|将采样事件和间隔更改为 `Config` 中指定的处理器性能计数器和间隔。|

## <a name="control-data-collection"></a>控制数据收集
 在目标应用程序运行时，可以通过使用 *VSPerfCmd.exe* 选项开始和停止向探查器数据文件写入数据，从而控制数据收集。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 以下选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|说明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 (**/globalon**) 或停止 (**/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|对由 `PID` 指定的进程，启动 (/processon) 或停止 (/processoff) 数据收集。|
    |[/attach](../profiling/attach.md) **:**{`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[**:**{`PID`&#124;`ProcName`}]|/attach 将启动由 `PID` 或进程名称 (ProcName) 指定的进程的数据收集。 **/detach** 将停止指定进程或所有进程（未指定任何特定进程时）的数据收集。|

## <a name="end-the-profiling-session"></a>结束分析会话
 若要结束分析会话，必须将探查器与所有被分析进程分离，并且必须显式关闭探查器。 可通过关闭应用程序或调用 **VSPerfCmd /detach** 选项从使用采样方法分析的应用程序分离探查器。 然后，调用 **VSPerfCmd /shutdown** 选项关闭探查器和分析数据文件。 **VSPerfClrEnv /off** 命令会清除分析环境变量。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 执行下列步骤之一，从目标应用程序分离探查器：

    - 键入 **VSPerfCmd /detach**

         或

    - 关闭目标应用程序。

2. 关闭探查器。 类型：

     **VSPerfCmd** [/shutdown](../profiling/shutdown.md)

3. （可选）清除分析环境变量。 类型：

     **VSPerfClrEnv /off**

## <a name="see-also"></a>请参阅
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [采样方法数据视图](../profiling/profiler-sampling-method-data-views.md)