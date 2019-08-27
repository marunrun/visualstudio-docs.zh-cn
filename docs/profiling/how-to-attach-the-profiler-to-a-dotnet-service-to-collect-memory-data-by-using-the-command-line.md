---
title: 将探查器附加到 .NET 服务以收集内存数据
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: aeac39af-ad99-479f-aa36-4104356ca512
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: fa054367ee8953c433512b6c4bcb0964637a1b74
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66746289"
---
# <a name="how-to-attach-the-profiler-to-a-net-service-to-collect-memory-data-by-using-the-command-line"></a>如何：将探查器附加到 .NET 服务，以使用命令行收集内存数据
本文介绍如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具将探查器附加 .NET Framework 服务并收集内存数据。 可以收集有关内存分配数量和大小的数据，还可以收集有关内存对象生存期的数据。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。
>
> [!NOTE]
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

 要从 .NET Framework 服务收集内存数据，请在托管服务的计算机上使用 [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) 工具初始化适当的环境变量。 必须重新启动该计算机才能配置它进行分析。

 随后使用 [VSPerfCmd](../profiling/vsperfcmd.md) 工具将探查器附加到服务进程。 将探查器附加到服务时，可以暂停和恢复数据收集。

 若要结束分析会话，必须将探查器与服务拆离，并且必须显式关闭探查器。 在大多数情况下，建议在会话结束时清除分析环境变量。

## <a name="attach-the-profiler"></a>附加探查器

#### <a name="to-attach-the-profiler-to-a-net-framework-service"></a>将探查器附加到 .NET Framework 服务

1. 必要时请安装该服务。

2. 打开命令提示符窗口。

3. 初始化分析环境变量。 类型：

    **VSPerfClrEnv** { **/globalsamplegc /globalsamplegclife**}[ **/samplelineoff**]

   - /globalsamplegclife  和 /globalsamplegclife  选项指定要收集的内存数据类型。 指定下列选项中的一个且仅指定一个。

     **/globalsamplegc** 启用对内存分配数据的收集。

     **/globalsamplegclife** 启用对内存分配数据和对象生存期数据的收集。

   - /samplelineoff  选项禁用源代码行号数据的收集。

4. 重启计算机，设置新的环境配置。

5. 必要时，请启动该服务。

6. 打开命令提示符窗口。 如有必要，将探查器路径添加到 PATH 环境变量。

7. 启动探查器。 类型：

    **VSPerfCmd**  [/start](../profiling/start.md) **:sample**  [/output](../profiling/output.md) **:** `OutputFile` [`Options`]

   - /start:sample  选项初始化探查器。

   - **/output:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置。

     可以将以下一个或多个选项与 /start:sample  选项一起使用。

   > [!NOTE]
   > **/User** 和 **/crosssession** 选项通常为服务所需选项。

   | 选项 | 说明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | 指定拥有进程的帐户的域和用户名。 在进程以已登录用户外的用户身份运行时才需要此选项。 进程所有者在 Windows 任务管理器的“进程”选项卡上的“用户名”列中列出。 |
   | [/crosssession](../profiling/crosssession.md) | 启用其他登录会话中的进程分析。 如果 ASP.NET 应用程序在其他会话中运行，则需要此选项。 会话 ID 在 Windows 任务管理器的“进程”选项卡上的“会话 ID”列中列出。 可以将 **/CS** 指定为 **/crosssession** 的缩写。 |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | 指定用于运行服务的登录帐户的可选域和用户名。 登录帐户会在 Windows 服务控制管理器中服务的“登录身份”列中列出。 |
   | [/crosssession&#124;cs](../profiling/crosssession.md) | 启用其他登录会话中的进程分析。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | 指定要在分析期间收集的 Windows 性能计数器。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | 指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中。 |

8. 将探查器附加到该服务。 类型：

    **VSPerfCmd**  [/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [[/targetclr](../profiling/targetclr.md) **:** `Version`]

   - 指定服务的进程 ID 或进程名称。 可以在 Windows 任务管理器中查看所有运行中的进程的进程 ID 和名称。

   - **targetclr:** `Version` 指定应用程序中加载运行时的多个版本时要分析的公共语言运行时 (CLR) 的版本。 可选。

## <a name="control-data-collection"></a>控制数据收集
 服务运行时，可使用 VSPerfCmd.exe  选项停止或开始将数据写入到探查器数据文件。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 以下 **VSPerfCmd** 选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|说明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|
    |**/attach:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[:{`PID`&#124;`ProcName`}]|**/attach** 将启动由进程 ID 或进程名称指定的进程的数据收集。 **/detach** 将停止指定进程或所有进程（未指定特定进程时）的数据收集。|

## <a name="end-the-profiling-session"></a>结束分析会话
 若要结束分析会话，探查器不得再收集数据。 可通过停止服务或调用 VSPerfCmd /detach  选项，停止从使用采样方法分析的应用程序收集数据。 然后，调用 VSPerfCmd  [/shutdown](../profiling/shutdown.md) 选项关闭探查器和分析数据文件。 **VSPerfClrEnv /globaloff** 命令可清除分析环境变量，但在重新启动计算机前不会重置系统配置。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 执行下列操作之一以从目标应用程序中拆离探查器：

    - 停止服务。

         或

    - 键入 **VSPerfCmd /detach**

2. 关闭探查器。 类型：

     **VSPerfCmd /shutdown**

3. （可选）清除分析环境变量。 类型：

     VSPerfClrEnv /globaloff 

4. 重新启动计算机。

## <a name="see-also"></a>请参阅
- [分析服务](../profiling/command-line-profiling-of-services.md)
- [.NET 内存数据视图](../profiling/dotnet-memory-data-views.md)