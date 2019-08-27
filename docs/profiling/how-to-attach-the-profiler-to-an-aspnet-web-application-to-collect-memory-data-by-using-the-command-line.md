---
title: 将探查器附加到 ASP.NET 应用以收集内存数据
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d608f85a-41ae-4ca7-85e6-b96624dbc83c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: b6caca91849727fa21fec0401c776e4c80f9a6b3
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63439526"
---
# <a name="how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-memory-data-by-using-the-command-line"></a>如何：将探查器附加到 ASP.NET Web 应用程序，以使用命令行收集内存数据
本文介绍如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具将探查器附加到 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序，以及如何收集有关 .NET Framework 内存分配数量和大小的数据。 也可以收集有关 .NET Framework 内存对象生存期的数据。

> [!NOTE]
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

 若要从 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序收集性能数据，请在承载 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序的计算机上使用 [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) 工具初始化相应的环境变量。 您必须重新启动计算机以配置 Web 服务器进行分析。

 然后，使用 [VSPerfCmd.exe](../profiling/vsperfcmd.md) 工具将探查器附加到承载网站的 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程。 将探查器附加到应用程序时，可以暂停和恢复数据收集。

 若要结束分析会话，探查器不得再附加于应用程序，并且必须显示关闭探查器。 在大多数情况下，建议在会话结束时清除分析环境变量。

## <a name="attach-the-profiler"></a>附加探查器

#### <a name="to-attach-the-profiler-to-an-aspnet-web-application"></a>将探查器附加到 ASP.NET Web 应用程序

1. 打开一个命令提示符窗口。

2. 初始化分析环境变量。 类型：

    **VSPerfClrEnv** {**/globalsamplegc** &#124; **/globalsamplegclife**} [**/samplelineoff**]

   - /globalsamplegc 和 /globalsamplegclife 选项指定要收集的内存数据类型。

        指定下列选项中的一个且仅指定一个。

       |选项|说明|
       |------------|-----------------|
       |/globalsamplegc|启用对内存分配数据的收集。|
       |/globalsamplegclife|启用对内存分配数据和对象生存期数据的收集。|

   - /samplelineoff 选项禁用向特定源代码行分配收集的数据。 如果指定此选项，则在函数级别分配数据。

3. 重启计算机，设置新的环境配置。

4. 打开一个命令提示符窗口。 如有必要，设置探查器路径环境变量。

5. 启动探查器。 类型：

    **VSPerfCmd**  [/start](../profiling/start.md) **:sample**  [/output](../profiling/output.md) **:** `OutputFile` [`Options`]

   - /start:sample 选项初始化探查器。

   - **/output:**`OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置。

     可以将以下任意选项与 **/start:sample** 选项一起使用。

   > [!NOTE]
   > **/user** 和 **/crosssession** 选项通常为 ASP.NET 应用程序所需选项。

   | 选项 | 说明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` | 指定拥有 ASP.NET 工作进程的帐户的域和用户名。 在进程以已登录用户外的用户身份运行时才需要此选项。 进程所有者在 Windows 任务管理器的“进程”选项卡上的“用户名”列中列出。 |
   | [/crosssession](../profiling/crosssession.md) | 启用其他登录会话中的进程分析。 如果 ASP.NET 应用程序在其他会话中运行，则需要此选项。 会话标识符在 Windows 任务管理器的“进程”选项卡上的“会话 ID”列中列出。 可以将 **/CS** 指定为 **/crosssession** 的缩写。 |
   | [/waitstart](../profiling/waitstart.md) [**:**`Interval`] | 指定探查器返回错误前，等待探查器初始化的秒数。 如果未指定 `Interval`，则探查器将无限期等待。 默认情况下，/start 将立即返回。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | 指定要在分析期间收集的 Windows 性能计数器。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | 指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中。 |

6. 以典型方式启动 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序。

7. 将探查器附加到 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程。 类型：

    **VSPerfCmd**  [/attach](../profiling/attach.md) **:**{`PID`&#124;`ProcName`} [[/targetclr](../profiling/targetclr.md)**:**`Version`]

   - 进程 ID `(PID)` 指定 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程的进程 ID 或进程名称。 可以在 Windows 任务管理器中查看所有运行中的进程的进程 ID。

   - /targetclr：`Version` 指定应用程序中加载运行时的多个版本时要分析的公共语言运行时 (CLR) 的版本。

## <a name="control-data-collection"></a>控制数据收集
 在应用程序运行时，可以使用 VSPerfCmd.exe 选项开始和停止向探查器数据文件写入数据，从而控制数据收集。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 以下 **VSPerfCmd** 选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|说明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 (**/globalon**) 或停止 (**/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 (**/processon**) 或停止 (**/processoff**) 由 `PID` 指定的进程的数据收集。|
    |**/attach:**{`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[**:**{`PID`&#124;:`ProcName`}]|/attach 将启动由进程 ID 或进程名称指定的进程的数据收集。 **/detach** 将停止指定进程或所有进程（未指定任何特定进程时）的数据收集。|

## <a name="end-the-profiling-session"></a>结束分析会话
 若要结束分析会话，必须从 Web 应用程序分离探查器。 可通过重启 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程或调用 VSPerfCmd /detach 选项，停止从使用采样方法分析的应用程序收集数据。 然后，可以调用 VSPerfCmd [/shutdown](../profiling/shutdown.md) 选项，关闭探查器和分析数据文件。 **VSPerfClrEnv /globaloff** 命令可清除分析环境变量，但在重新启动计算机前不会重置系统配置。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 执行下列步骤之一，从目标应用程序分离探查器：

   - 键入 VSPerfCmd [/detach](../profiling/detach.md)

      或

   - 关闭 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程。 类型：

     **IISReset /stop**

2. 关闭探查器。 类型：

    **VSPerfCmd /shutdown**

3. （可选）清除分析环境变量。 类型：

    **VSPerfCmd /globaloff**

4. 重新启动计算机。 如有必要，重启 Internet Information Services (IIS)。 类型：

    **IISReset /start**

## <a name="see-also"></a>请参阅
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [.NET 内存数据视图](../profiling/dotnet-memory-data-views.md)