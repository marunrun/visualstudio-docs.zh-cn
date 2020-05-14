---
title: 探查器命令行：检测本机服务，获取计时数据
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: dfe58b39-63f8-4a87-ab3a-2b5b14faa8d0
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- cplusplus
ms.openlocfilehash: c738a5183a7708c967192cf201e38a4f9384710e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74778864"
---
# <a name="how-to-instrument-a-native-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line"></a>如何：使用探查器命令行检测本机服务，并收集详细计时数据
本文介绍如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具检测本机 (C/C++) 服务并收集详细的计时数据。

> [!NOTE]
> 如果某服务在计算机启动之后无法重启（此类服务只能在操作系统启动时启动），则无法使用检测方法分析该服务。
>
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

 若要使用检测方法从本机服务收集详细计时数据，可使用 [VSInstr.exe](../profiling/vsinstr.md) 工具生成该组件的受检测版本。 然后，将该服务的非检测版本替换为检测版本，确保将该服务配置为手动启动。 然后启动探查器。

 启动该服务时，会自动将计时数据收集到数据文件中。 在分析会话过程中可以暂停和恢复数据收集。

 若要结束分析会话，可关闭该服务，然后显式关闭探查器。

## <a name="start-the-application-with-the-profiler"></a>用探查器启动应用程序

#### <a name="to-start-profiling-a-native-service"></a>开始分析本机服务

1. 打开命令提示符窗口。

2. 使用 VSInstr  工具生成该服务二进制文件的检测版本。

3. 使用检测版本替换原始二进制文件。 在 Windows 服务控制管理器中，确保将该服务的“启动类型”设置为“手动”。

4. 启动探查器。 类型：

    **VSPerfCmd** [/start](../profiling/start.md) **:trace**  [/output](../profiling/output.md) **:** `OutputFile` [`Options`]

   - **/start:trace** 选项初始化探查器。

   - **/output:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置  。

     可以将以下任意选项与 **/start:trace** 选项一起使用。

   > [!NOTE]
   > **/user** 和 **/crosssession** 选项通常为 ASP.NET 应用程序所需选项。

   | 选项 | 描述 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | 指定拥有 ASP.NET 工作进程的帐户的域和用户名。 在进程以已登录用户外的用户身份运行时才需要此选项。 进程所有者在 Windows 任务管理器的“进程”选项卡上的“用户名”列中列出   。 |
   | [/crosssession](../profiling/crosssession.md) | 启用其他登录会话中的进程分析。 如果 ASP.NET 应用程序在其他会话中运行，则需要此选项。 会话 ID 位于 Windows 任务管理器的“进程”选项卡上的“会话 ID”列中。 可以将 **/CS** 指定为 **/crosssession** 的缩写。 |
   | [/waitstart](../profiling/waitstart.md)[ **:** `Interval`] | 指定探查器返回错误前，等待探查器初始化的秒数。 如果未指定 `Interval`，则探查器将无限期等待。 默认情况下，  /start 将立即返回。 |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | 若要启动探查器而暂停数据收集，请将 **/globaloff** 选项添加到 **/start** 命令行。 使用 **/globalon** 可恢复分析。 |
   | [/counter](../profiling/counter.md) **:** `Config` | 从 Config 中所指定的处理器性能计数器收集信息。计数器信息将添加到在每个分析事件中收集的数据中。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | 指定要在分析期间收集的 Windows 性能计数器。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | 指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中  。 |

5. 从服务控制管理器启动服务。

## <a name="control-data-collection"></a>控制数据收集
 服务运行时，可使用 VSPerfCmd.exe  选项开始或停止将数据写入到探查器数据文件。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭服务）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 以下 **VSPerfCmd** 选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|描述|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|启动 ( **/threadon**) 或停止 ( **/threadoff**) 由线程 ID (`TID`) 指定的线程的数据收集。|

## <a name="end-the-profiling-session"></a>结束分析会话
 若要结束分析会话，请停止正在运行受检测组件的服务，然后调用 VSPerfCmd  [/shutdown](../profiling/shutdown.md) 选项来关闭探查器和分析数据文件。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 从服务控制管理器停止服务。

2. 关闭探查器。 类型：

     **VSPerfCmd /shutdown**

3. 使用原始模块替换被检测模块。 如有必要，重新配置服务的“启动类型”。

## <a name="see-also"></a>请参阅
- [分析服务](../profiling/command-line-profiling-of-services.md)
- [检测方法数据视图](../profiling/instrumentation-method-data-views.md)
