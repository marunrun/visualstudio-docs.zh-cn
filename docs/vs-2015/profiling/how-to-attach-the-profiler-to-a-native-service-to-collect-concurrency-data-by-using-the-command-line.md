---
title: 如何：使用命令行将探查器附加到本机服务以收集并发数据 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 283a1ee1-b43e-4daf-95ae-1311925a42a8
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ab6e56d6b2d9a953b5549d59ea85049be8cc0306
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432886"
---
# <a name="how-to-attach-the-profiler-to-a-native-service-to-collect-concurrency-data-by-using-the-command-line"></a>如何：Profiler 附加到本机服务以使用命令行收集并发数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题介绍如何使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分析工具命令行工具将探查器附加到本机 (C/C++) 服务并使用采样方法收集进程和线程并发数据。  

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 Windows 应用商店应用程序也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。  

> [!NOTE]
> 分析工具的命令行工具位于 Visual Studio 安装目录的 \Team Tools\Performance Tools 子目录中。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要在命令提示符下使用探查器，必须将工具路径添加到**命令提示符**窗口的 PATH 环境变量中，或将其添加到命令本身。 有关详细信息，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。  

 将探查器附加到服务时，可以暂停和恢复数据收集。 若要结束分析会话，探查器不得再附加于服务，且须显示关闭探查器。  

## <a name="attaching-the-profiler"></a>附加探查器  
 若要将探查器附加到本机服务，请使用 **VSPerfCmd/start** 和 **/attach** 选项初始化探查器，并将其附加到目标应用程序。 可以在单个命令行中指定 **/start** 和 **/attach** 及其各自的选项。 还可以添加 **/globaloff** 选项，以在目标应用程序启动时暂停数据收集。 然后可使用 **/globalon** 开始收集数据。  

#### <a name="to-attach-the-profiler-to-a-native-service"></a>将探查器附加到本机服务  

1. 如果服务未运行，请启动该服务。  

2. 在命令提示符中键入以下内容以启动探查器：  

    [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency   /output:** `OutputFile` [`Options`]  

   - [/output](../profiling/output.md)**:**`OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置。  

     可将下表中的任意选项与 **/start** 选项一起使用。  

   > [!NOTE]
   > 大多数服务都需要 **/user** 和 **/crosssession** 选项。  

   |                               选项                               |                                                                     描述                                                                      |
   |--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain\`]`UserName` |                           指定要向探查器授予访问权限的帐户的可选域和用户名。                           |
   |           [/crosssession](../profiling/crosssession.md)            |                                               启用其他登录会话中的进程分析。                                                |
   |  [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`  |                                      指定要在分析期间收集的 Windows 性能计数器。                                       |
   |       [/automark](../profiling/automark.md) **:** `Interval`       | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500。 |
   |     [/events](../profiling/events-vsperfcmd.md) **:** `Config`     |       指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中。       |

3. 在命令提示符中键入以下命令以将探查器附加到服务：  

    **VSPerfCmd /attach:** `PID`  

    `PID` 指定目标应用程序的进程 ID 或进程名称。 可以在 Windows 任务管理器中查看所有运行中的进程的进程 ID。  

## <a name="controlling-data-collection"></a>控制数据收集  
 目标应用程序运行时，可通过使用 VSPerfCmd.exe 选项开始和停止向文件写入数据，从而控制数据收集。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。  

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集  

- 下表中的选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。  

    |选项|描述|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 (**/globalon**) 或停止 (**/globaloff**) 所有进程的数据收集。|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 (**/processon**) 或停止 (**/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|  
    |[/attach](../profiling/attach.md) **:**{`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[**:**{`PID`&#124;`ProcName`}]|**/attach** 将启动由进程 ID (`PID`) 或进程名称 (*ProcName*) 指定的进程的数据收集。 **/detach** 将停止指定进程或所有进程（未指定任何特定进程时）的数据收集。|  

## <a name="ending-the-profiling-session"></a>结束分析会话  
 若要结束分析会话，探查器不得再收集数据。 可通过停止服务或调用 **VSPerfCmd /detach** 选项从使用并发方法分析的本机服务停止数据收集。 然后，可以调用 **VSPerfCmd /shutdown** 选项关闭探查器和分析数据文件。  

#### <a name="to-end-a-profiling-session"></a>结束分析会话  

1. 通过停止服务或在命令提示符中键入以下命令将探查器与目标应用程序分离：  

     键入 **VSPerfCmd /detach**  

2. 在命令提示符下键入以下命令以关闭探查器：  

     **VSPerfCmd** [/shutdown](../profiling/shutdown.md)
