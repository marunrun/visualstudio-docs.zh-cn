---
title: 如何：将 Profiler 附加到 ASP.NET Web 应用程序以使用命令行收集应用程序统计信息 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 3725ddbe-ce91-4469-991e-8c5ed048c618
caps.latest.revision: 38
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5c60e63384ab6f391cee1151c8ee20d39ae2e1b2
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432858"
---
# <a name="how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-application-statistics-by-using-the-command-line"></a>如何：将 Profiler 附加到 ASP.NET Web 应用程序以使用命令行收集应用程序统计信息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题介绍如何使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分析工具命令行工具将探查器附加 ASP.NET Web 应用程序，以及如何使用采样方法收集性能统计信息。  

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 Windows 应用商店应用程序也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。  
>   
> 若要将层交互数据添加到分析运行，需要使用命令行分析工具执行特定的步骤。 请参阅[收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md)。  
>   
> 分析工具的命令行工具位于 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 安装目录的 \Team Tools\Performance Tools 子目录中。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。 有关详细信息，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。  

 若要从 ASP.NET Web 应用程序收集性能数据，必须初始化适当的环境变量，并且必须重新启动承载 ASP.NET Web 应用程序的计算机，才能配置 Web 服务器进行分析。  

 随后将探查器附加到承载网站的 ASP.NET 工作进程。 将探查器附加到应用程序时，可以暂停和恢复数据收集。  

 若要结束分析会话，必须将探查器与所有被分析应用程序拆离，并且必须显式关闭探查器。 在大多数情况下，建议在会话结束时清除分析环境变量。  

## <a name="starting-the-profiler-and-attaching-to-an-aspnet-web-application"></a>启动探查器并附加到 ASP.NET Web 应用程序  

#### <a name="to-attach-the-profiler-to-an-aspnet-web-application"></a>将探查器附加到 ASP.NET Web 应用程序  

1. 打开命令提示符窗口。  

2. 初始化分析环境变量。 类型：  

    **VSPerfClrEnv /globalsampleon** [**/samplelineoff**]  

   - **/globalsampleon** 启用采样。  

   - **/samplelineoff** 禁用向特定源代码行分配收集的数据。 指定此选项时，仅向函数分配数据。  

3. 重新启动计算机。  

4. 启动探查器。 输入：**VSPerfCmd** [/start](../profiling/start.md)**:sample** [/output](../profiling/output.md)**:**`OutputFile`[`Options`]  

   - /start:sample 选项初始化探查器。  

   - **/output:**`OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置。  

     可以将以下任意选项与 /start:sample 选项一起使用。  

   > [!NOTE]
   > **/user** 和 **/crosssession** 选项通常为 ASP.NET 应用程序所需选项。  

   |                                 选项                                  |                                                                                                                                                        描述                                                                                                                                                        |
   |-------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` |                   指定拥有 ASP.NET 工作进程的帐户的域和用户名。 在进程以已登录用户外的用户身份运行时才需要此选项。 进程所有者在 Windows 任务管理器的“进程”选项卡上的“用户名”列中列出。                    |
   |              [/crosssession](../profiling/crosssession.md)              | 启用其他登录会话中的进程分析。 如果 ASP.NET 应用程序在其他会话中运行，则需要此选项。 会话标识符在 Windows 任务管理器的“进程”选项卡上的“会话 ID”列中列出。 可以将 **/CS** 指定为 **/crosssession** 的缩写。 |
   |    [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`     |                                                                                                                         指定要在分析期间收集的 Windows 性能计数器。                                                                                                                         |
   |         [/automark](../profiling/automark.md) **:** `Interval`          |                                                                                       仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。                                                                                       |
   |       [/events](../profiling/events-vsperfcmd.md) **:** `Config`        |                                                                                         指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中。                                                                                          |

5. 以典型方式启动 ASP.NET Web 应用程序。  

6. 将探查器附加到 ASP.NET 工作进程。 输入：**VSPerfCmd** [/attach](../profiling/attach.md)**:**{`PID`&#124;`ProcName`} [`Sample Event`] [[/targetclr](../profiling/targetclr.md)**:**`Version`]  

   - `PID` 指定 ASP.NET 工作进程的进程 ID；`ProcName` 指定工作进程的名称。 可以在 Windows 任务管理器中查看所有运行中的进程的进程 ID 和名称。  

   - 默认情况下，性能数据为每 10,000,000 个非暂停处理器时钟周期采样一次。 在 1GH 处理器上，每秒约为 100 次。 可以指定以下 VSPerfCmd 选项之一，更改时钟周期间隔或指定不同的采样事件。  

   |样本事件|描述|  
   |------------------|-----------------|  
   |[/timer](../profiling/timer.md) **:** `Interval`|将采样间隔更改为 `Interval` 所指定的非暂停时钟周期数目。|  
   |[/pf](../profiling/pf.md)[**:**`Interval`]|将采样事件更改为页面错误。 如果已指定 `Interval`，则会设置样本之间的页面错误数目。 默认值为 10。|  
   |[/sys](../profiling/sys-vsperfcmd.md)[`:``Interval`]|将采样事件更改为从进程对操作系统内核的系统调用 (syscall)。 如果已指定 `Interval`，则会设置样本之间的调用次数。 默认值为 10。|  
   |[/counter](../profiling/counter.md) **:** `Config`|将采样事件和间隔更改为 `Config` 中指定的处理器性能计数器和间隔。|  
   |[/targetclr](../profiling/targetclr.md) **:** `Version`|指定应用程序中加载公共语言运行时 (CLR) 的多个版本时要分析的运行时的版本。|  

   - **targetclr:** `Version` 指定应用程序中加载运行时的多个版本时要分析的 CLR 版本。 可选。  

## <a name="controlling-data-collection"></a>控制数据收集  
 应用程序运行时，可以使用 VSPerfCmd.exe 选项开始和停止向文件写入数据，从而控制数据收集。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。  

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集  

- 以下 **VSPerfCmd** 选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。  

    |选项|描述|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 (**/globalon**) 或停止 (**/globaloff**) 所有进程的数据收集。|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` **/processoff:** `PID`|对由 `PID` 指定的进程，启动 (/processon) 或停止 (/processoff) 数据收集。|  
    |[/attach](../profiling/attach.md) **:**{`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[**:**{`PID`&#124;`ProcName`}]|**/attach** 将启动由 `PID` 或进程名称 (ProcName) 指定的进程的数据收集。 **/detach** 将停止指定进程或所有进程（未指定任何特定进程时）的数据收集。|  

## <a name="ending-the-profiling-session"></a>结束分析会话  
 要结束分析会话，请关闭 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web 应用，然后使用 Internet Information Services (IIS) IISReset 命令来关闭 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 工作进程。 调用 VSPerfCmd [/shutdown](../profiling/shutdown.md) 选项关闭探查器和分析数据文件。  

 VSPerfClrEnv /globaloff 命令会清除分析环境变量。 必须重启计算机才能应用新的环境设置。  

 **VSPerfClrEnv /globaloff** 命令可清除分析环境变量，但在重新启动计算机前不会重置系统配置。  

#### <a name="to-end-a-profiling-session"></a>结束分析会话  

1. 执行下列操作之一以从目标应用程序中拆离探查器：  

    - 键入 **VSPerfCmd /detach**  

         或  

    - 关闭 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 工作进程。  

2. 关闭探查器。 输入：**VSPerfCmd** [/shutdown](../profiling/shutdown.md)  

3. （可选）清除分析环境变量。 类型：  

     **VSPerfCmd /globaloff**  

4. 重新启动计算机。  

## <a name="see-also"></a>请参阅  
 [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [采样方法数据视图](../profiling/profiler-sampling-method-data-views.md)
