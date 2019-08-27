---
title: 如何：将 Profiler 附加到 ASP.NET Web 应用程序以使用命令行收集并发数据 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 0e215fdd-55f8-43ef-9534-06542eefe223
caps.latest.revision: 34
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d720779019ab4106fa6c4b727e9994f168a2d8f2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68179286"
---
# <a name="how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-concurrency-data-by-using-the-command-line"></a>如何：将 Profiler 附加到 ASP.NET Web 应用程序以使用命令行收集并发数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题介绍如何使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分析工具命令行工具将探查器附加到 ASP.NET Web 应用程序并收集进程和线程并发数据。  

 分析工具的命令行工具位于 Visual Studio 安装目录的 \Team Tools\Performance Tools 子目录中。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要在命令提示符下使用探查器，必须将工具路径添加到**命令提示符**窗口的 PATH 环境变量中，或将其添加到命令本身。 有关详细信息，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。  

 若要收集并发数据，请将探查器附加到承载 Web 站点的 ASP.NET 工作进程。 将探查器附加到应用程序时，可以暂停和恢复数据收集。 若要结束分析会话，探查器不得再附加于应用程序，并且必须显示关闭探查器。 在大多数情况下，应该在会话结束时清除分析环境变量。  

## <a name="attaching-the-profiler"></a>附加探查器  

#### <a name="to-attach-the-profiler-to-a-aspnet-application"></a>将探查器附加到 ASP.NET 应用程序  

1. 通过键入以下命令启动探查器：  

    [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency /output:** `OutputFile` [`Options`]  

   - [/start](../profiling/start.md) 选项将初始化探查器以收集资源争用数据。  

   - [/output](../profiling/output.md) **:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置。  

     可将下表中的任意选项与 **/start** 选项一起使用。  

   |                               选项                               |                                                                     描述                                                                      |
   |--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain\`]`UserName` |                           指定要向探查器授予访问权限的帐户的可选域和用户名。                           |
   |           [/crosssession](../profiling/crosssession.md)            |                                               启用其他登录会话中的进程分析。                                                |
   |  [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`  |                                      指定要在分析期间收集的 Windows 性能计数器。                                       |
   |       [/automark](../profiling/automark.md) **:** `Interval`       | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500。 |
   |     [/events](../profiling/events-vsperfcmd.md) **:** `Config`     |       指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中。       |

2. 以典型方式启动 ASP.NET 应用程序。  

3. 通过键入以下命令将探查器附加到 ASP.NET 工作进程：**VSPerfCmd /attach:** `PID` [ **/targetclr:** `Version`]  

   - `PID` 指定 ASP.NET 工作进程的 ID 或名称。 可以在 Windows 任务管理器中查看所有运行中的进程的进程 ID。  

   - [/targetclr](../profiling/targetclr.md) **:** `Version` 指定应用程序中加载运行时的多个版本时要分析的公共语言运行时 (CLR) 的版本。 此参数可选。  

## <a name="controlling-data-collection"></a>控制数据收集  
 应用程序运行时，可以通过使用 VSPerfCmd.exe 选项开始和停止向文件写入数据，从而控制数据收集。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。  

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集  

- 下表中的 VSPerfCmd 选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。  

    |选项|描述|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|  
    |[/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[ **:** {`PID`&#124;`ProcName`}]|**/attach** 将启动由进程 ID (`PID`) 或进程名称 (*ProcName*) 指定的进程的数据收集。 **/detach** 将停止指定进程或所有进程（未指定任何特定进程时）的数据收集。|  

## <a name="ending-the-profiling-session"></a>结束分析会话  
 若要结束分析会话，探查器不得再收集数据。 可通过重新启动 ASP.NET 工作进程或调用 **VSPerfCmd /detach** 选项从使用并发方法分析的应用程序停止数据收集。 然后，可以调用 **VSPerfCmd /shutdown** 选项关闭探查器和分析数据文件。 **VSPerfClrEnv /globaloff** 命令可清除分析环境变量，但在重新启动计算机前不会重置系统配置。  

#### <a name="to-end-a-profiling-session"></a>结束分析会话  

1. 通过将其关闭或在命令提示符中键入以下命令将探查器与目标应用程序分离：  

     **VSPerfCmd /detach**  

2. 在命令提示符下键入以下命令以关闭探查器：  

     **VSPerfCmd** [/shutdown](../profiling/shutdown.md)  

## <a name="see-also"></a>请参阅  
 [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [使用 VSPerfASPNETCmd 进行快速网站分析](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)
