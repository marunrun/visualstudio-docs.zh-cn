---
title: VSPerfCmd：将探查器附加到本机服务以获取应用统计信息
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f783817f-77a0-4eb8-985b-ec3b77eadc42
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 10dfd24a0864cf3f0564e657e22c68a88eb3af8d
ms.sourcegitcommit: 91c7f1b525e0c22d938bc4080ba4ceac2483474f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2019
ms.locfileid: "67033157"
---
# <a name="how-to-attach-the-profiler-to-a-native-service-to-collect-application-statistics-by-using-the-command-line"></a>如何：将探查器附加到本机服务，以使用命令行收集应用程序统计信息
本文介绍如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具将探查器附加本机服务，以及如何使用采样方法收集性能统计信息。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。
>
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

 将探查器附加到服务时，可以暂停和恢复数据收集。

 若要结束分析会话，必须将探查器与服务拆离，并且必须显式关闭探查器。

## <a name="start-the-application-with-the-profiler"></a>用探查器启动应用程序
 若要将探查器附加到本机服务，请使用 VSPerfCmd.exe  [/start](../profiling/start.md) 和 [/attach](../profiling/attach.md) 选项初始化探查器，并将其附加到目标应用程序。 可以在单个命令行中指定 **/start** 和 **/attach** 及其各自的选项。 还可以添加 [/globaloff](../profiling/globalon-and-globaloff.md) 选项，以在目标应用程序启动时暂停数据收集。 然后可使用 [/globalon](../profiling/globalon-and-globaloff.md) 开始收集数据。

#### <a name="to-attach-the-profiler-to-a-native-service"></a>将探查器附加到本机服务

1. 必要时，请启动该服务。

2. 打开命令提示符窗口。

3. 启动探查器。 类型：

    **VSPerfCmd /start:sample**  [/output](../profiling/output.md) **:** `OutputFile` [`Options`]

   - /start:sample  选项初始化探查器。

   - **/output:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置  。

     可以将以下任意选项与 **/start:sample** 选项一起使用。

   > [!NOTE]
   > **/User** 和 **/crosssession** 选项通常为服务所需选项。

   | 选项 | 说明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | 指定拥有所分析进程的帐户的域和用户名。 仅在进程以已登录用户外的用户身份运行时才需要此选项。 进程所有者在 Windows 任务管理器的“进程”选项卡上的“用户名”列中列出。 |
   | [/crosssession](../profiling/crosssession.md) | 启用其他会话中的进程分析。 如果应用程序在其他会话中运行，则需要此选项。 会话 ID 在 Windows 任务管理器的“进程”选项卡上的“会话 ID”列中列出。 可以将 **/CS** 指定为 **/crosssession** 的缩写。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | 指定要在分析期间收集的 Windows 性能计数器。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | 指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中。 |

4. 将探查器附加到该服务。 类型：

    **VSPerfCmd /attach:** `PID` [`Sample Event`]

    `PID` 指定目标应用程序的进程 ID。 可以在 Windows 任务管理器中查看所有运行中的进程的进程 ID。

    默认情况下，性能数据为每 10,000,000 个非暂停处理器时钟周期采样一次。 在 1GH 处理器上，大约每 10 秒钟一次。 可以指定以下选项之一，更改时钟周期间隔或指定不同的采样事件。

   |样本事件|说明|
   |------------------|-----------------|
   |[/timer](../profiling/timer.md) **:** `Interval`|将采样间隔更改为 `Interval` 所指定的非暂停时钟周期数目。|
   |[/pf](../profiling/pf.md)[ **:** `Interval`]|将采样事件更改为页面错误。 如果已指定 `Interval`，则会设置样本之间的页面错误数目。 默认值为 10。|
   |[/sys](../profiling/sys-vsperfcmd.md) [ **:** `Interval`]|将采样事件更改为从进程对操作系统内核的系统调用 (syscall)。 如果已指定 `Interval`，则会设置样本之间的调用次数。 默认值为 10。|
   |[/counter](../profiling/counter.md) **:** `Config`|将采样事件和间隔更改为 `Config` 中指定的处理器性能计数器和间隔。|

## <a name="control-data-collection"></a>控制数据收集
 目标应用程序运行时，可使用 VSPerfCmd.exe  选项开始或停止将数据写入到探查器数据文件。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 以下 **VSPerfCmd** 选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|说明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|
    |**/attach:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[:{`PID`&#124;`ProcName`}]|**/attach** 将启动由进程 ID 或进程名称指定的进程的数据收集。 **/detach** 将停止指定进程或所有进程（未指定进程时）的数据收集。|

## <a name="end-the-profiling-session"></a>结束分析会话
 若要结束分析会话，必须将探查器与服务拆离，然后显式关闭探查器。 可通过停止服务或调用 VSPerfCmd /detach  选项拆离使用采样方法分析的本机服务。 然后，调用 VSPerfCmd  [/shutdown](../profiling/shutdown.md) 选项关闭探查器和分析数据文件。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 执行下列操作之一以从目标应用程序中拆离探查器：

    - 停止服务。

         -或-

    - 键入 **VSPerfCmd /detach**

2. 关闭探查器。 类型：

     **VSPerfCmd /shutdown**

## <a name="see-also"></a>请参阅
- [分析服务](../profiling/command-line-profiling-of-services.md)
- [采样方法数据视图](../profiling/profiler-sampling-method-data-views.md)