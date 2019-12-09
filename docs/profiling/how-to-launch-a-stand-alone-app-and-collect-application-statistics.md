---
title: 探查器命令行：启动独立应用程序，获取应用程序统计信息
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 52dcee2b-f178-4a76-bddc-e36c50bfcb78
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: fb6228592115091dc538dbe59c227a180e75aa10
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74775408"
---
# <a name="how-to-launch-a-stand-alone-application-with-the-profiler-and-collect-application-statistics-by-using-the-command-line"></a>如何：使用探查器启动独立应用程序，并通过命令行收集应用程序统计信息
本主题介绍如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具启动独立（客户端）应用程序，以及如何使用采样方法收集性能统计信息。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。
>
> 若要将层交互数据添加到分析运行，需要使用命令行分析工具执行特定的步骤。 请参阅[收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md)

 若要使用探查器命令行工具，必须将路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。 可以在安装有 Visual Studio 的计算机上，使用 Visual Studio 命令窗口运行分析工具。

1. 如果在安装有 Visual Studio 的计算机上运行分析工具，Visual Studio 命令窗口会设置正确的路径。 在“工具”  菜单上，选择“VS 命令提示符” 

> [!NOTE]
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

## <a name="start-the-application-with-the-profiler"></a>用探查器启动应用程序
 若要使用探查器来启动目标应用程序，请使用 VSPerfCmd **/start** 和 **/launch** 选项来初始化探查器并启动应用程序。 可以在单个命令行中指定 **/start** 和 **/launch** 及其各自的选项。

 还可以添加 **/globaloff** 选项，以在目标应用程序启动时暂停数据收集。 然后可使用 **/globalon** 开始收集数据。

#### <a name="to-start-an-application-by-using-the-profiler"></a>用探查器启动应用程序

1. 打开一个命令提示符窗口。

2. 启动探查器。 类型：

    **VSPerfCmd /start:sample /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) **:sample** 选项初始化探查器。

   - [/output](../profiling/output.md) **:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置。

     可以将以下任意选项与 **/start:sample** 选项一起使用。

   | 选项 | 说明 |
   | - | - |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | 指定要在分析期间收集的 Windows 性能计数器。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | 指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中  。 |

3. 启动目标应用程序。 Type:**VSPerfCmd /launch:** `appName` [`Options`] [`Sample Event`]

    可以将以下一个或多个选项与 **/launch** 选项一起使用。

   |选项|说明|
   |------------|-----------------|
   |[/args](../profiling/args.md) **:** `Arguments`|指定一个字符串，其中包含要传递给目标应用程序的命令行参数。|
   |[/console](../profiling/console.md)|在另一个窗口中启动目标命令行应用程序。|

    默认情况下，性能数据为每 10,000,000 个非暂停处理器时钟周期采样一次。 在 1GHz 的处理器上，大约每 10 秒钟一次。 可以指定以下选项之一，更改时钟周期间隔或指定不同的采样事件。

   |样本事件|说明|
   |------------------|-----------------|
   |[/timer](../profiling/timer.md) **:** `Interval`|将采样间隔更改为 `Interval` 所指定的非暂停时钟周期数目。|
   |[/pf](../profiling/pf.md)[ **:** `Interval`]|将采样事件更改为页面错误。 如果已指定 `Interval`，则会设置样本之间的页面错误数目。 默认值为 10。|
   |[/sys](../profiling/sys-vsperfcmd.md)[ **:** `Interval`]|将采样事件更改为从进程对操作系统内核的系统调用 (syscall)。 如果已指定 `Interval`，则会设置样本之间的调用次数。 默认值为 10。|
   |[/counter](../profiling/counter.md) **:** `Config`|将采样事件和间隔更改为 `Config` 中指定的处理器性能计数器和间隔。|

## <a name="control-data-collection"></a>控制数据收集
 在目标应用程序运行时，可以通过使用 *VSPerfCmd.exe* 选项开始和停止向探查器数据文件写入数据，从而控制数据收集。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 以下选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|说明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID`  [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|
    |[/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[ **:** {`PID`&#124;`ProcName`}]|**/attach** 将启动由 `PID` 或进程名称 (ProcName) 指定的进程的数据收集。 **/detach** 将停止指定进程或所有进程（未指定任何特定进程时）的数据收集。|

## <a name="end-the-profiling-session"></a>结束分析会话
 若要结束分析会话，探查器不得再附加于任何已分析的进程，且须显式关闭探查器。 可通过关闭应用程序或调用 **VSPerfCmd /detach** 选项从使用采样方法分析的应用程序分离探查器。 然后，调用 **VSPerfCmd /shutdown** 选项关闭探查器和分析数据文件。 **VSPerfClrEnv /off** 命令会清除分析环境变量。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 执行下列步骤之一，从目标应用程序分离探查器：

    - 关闭目标应用程序。

         -或-

    - 键入 **VSPerfCmd /detach**

2. 关闭探查器。 类型：

     **VSPerfCmd** [/shutdown](../profiling/shutdown.md)

## <a name="see-also"></a>请参阅
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [采样方法数据视图](../profiling/profiler-sampling-method-data-views.md)
