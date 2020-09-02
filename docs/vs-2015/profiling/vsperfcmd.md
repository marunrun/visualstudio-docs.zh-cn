---
title: VSPerfCmd | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- performance tools, VSPerfCmd tool
- command-line tools, VSPerfCmd tool
- command line, tools
- profiling tools,VSPerfCmd
- VSPerfCmd tool
ms.assetid: 778bc105-7643-46c4-a338-f3620e31125a
caps.latest.revision: 54
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: da82cbd8426b1a9af08e27577cdb76ca4a64d2e2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148217"
---
# <a name="vsperfcmd"></a>VSPerfCmd
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPerfCmd.exe 工具用于启动和停止性能数据收集。 它使用以下语法：  
  
```  
VSPerfCmd [/U] [/options]  
```  
  
 下表描述了 VSPerfCmd.exe 工具选项。  
  
|选项|描述|  
|------------|-----------------|  
|**U**|以 Unicode 形式写入重定向的控制台输出。 必须是指定的第一个选项。|  
|[Start](../profiling/start.md) **:** `mode`|在指定模式下启动分析服务。|  
|[Output](../profiling/output.md) **:** `filename`|指定输出文件名。 仅与 Start 一起使用。|  
|[CrossSession&#124;CS](../profiling/crosssession.md)|启用跨 Windows 会话的分析。 仅与 Start、Attach 或 Launch 一起使用。|  
|[User](../profiling/user-vsperfcmd.md) **:** [`domain\`]`username`|启用指定帐户访问探查器服务。 仅与 Start 一起使用。|  
|[WaitStart](../profiling/waitstart.md)[ **:** `n`]|等待要初始化的数据收集记录器。 如果已指定 `n`，则 VSPerfCmd 将最多等待 `n` 秒。 如果 `n` 未指定，则 VSPerfCmd 将无限期等待。 这简化了作为批处理过程一部分的 VSPerfCmd 的使用。|  
|[Counter](../profiling/counter.md) **:** `cfg`|使用示例分析方法时，指定 CPU 计数器和事件数，以用作采样间隔。 只能对一个计数器值进行采样。<br /><br /> 使用检测分析方法时，指定要在每个检测点收集的 CPU 计数器。 仅使用 "**开始时间：** `Trace` "、"**附加**" 或 "**启动**"。|  
|[QueryCounters](../profiling/querycounters.md)|显示当前计算机的有效 CPU 计数器列表。|  
|[WinCounter](../profiling/wincounter.md) **:** *path*|指定要与配置文件标记数据一起包括的 Windows 性能计数器事件。 仅与 Start 一起使用。|  
|[AutoMark](../profiling/automark.md) **:** *n*|指定 Windows 性能计数器数据收集事件之间的时间间隔（以毫秒为单位）。 与 WinCounter 一起使用。|  
|[Events](../profiling/events-vsperfcmd.md) **:** `option`|控制指定的 Windows 事件跟踪 (ETW) 事件的集合。 将 ETW 数据收集到不是分析数据 (.vsp) 文件的 .itl 文件中。|  
|[状态](../profiling/status.md)|显示探查器状态、当前正在分析的进程的信息以及有权控制探查器的帐户信息。|  
|[Shutdown](../profiling/shutdown.md)[ **:** `n`]|关闭分析数据文件并关闭探查器。|  
|[GlobalOn](../profiling/globalon-and-globaloff.md)|调用 VSPerfCmdGlobalOff 后恢复数据收集。|  
|[GlobalOff](../profiling/globalon-and-globaloff.md)|停止所有数据收集，但不结束分析会话。|  
|[ProcessOn](../profiling/processon-and-processoff.md) **:** `pid`|在通过调用 VSPerfCmdProcessOff 暂停分析后，恢复指定进程的数据收集。|  
|[ProcessOff](../profiling/processon-and-processoff.md) **:** `pid`|停止指定进程的数据收集。|  
|[ThreadOn and ThreadOff](../profiling/threadon-and-threadoff.md) **:** *tid*|在通过调用 VSPerfCmdThreadOff 暂停分析后，恢复对指定进程的分析。 仅在使用检测方法进行分析时使用 ThreadOn。|  
|[ThreadOn and ThreadOff](../profiling/threadon-and-threadoff.md) **:** *tid*|暂停对指定线程的分析。 仅在使用检测方法进行分析时使用“ThreadOff”。|  
|[Mark](../profiling/mark.md) **:** MarkNum[,MarkText]|使用可选文本将一个标记插入到分析数据文件中。|  
  
## <a name="sampling-method-options"></a>采样方法选项  
 只有在使用采样分析方法时才能使用以下选项。  
  
|选项|描述|  
|------------|-----------------|  
|[Launch](../profiling/launch.md) **:** 可执行文件|启动指定的应用程序并开始分析。|  
|[Args](../profiling/args.md) **:** 参数|指定要传递到已启动应用程序的命令行参数。|  
|[控制台](../profiling/console.md)|在新的命令提示符窗口中启动指定命令。|  
|[Attach](../profiling/attach.md) **:** PID[,PID]|开始分析指定进程。 进程可由进程 ID 或进程名称标识。|  
|[Detach](../profiling/detach.md)[ **:** _PID_[,_PID_]]|停止分析指定进程。 进程可由进程 ID 或进程名称标识。 如果未指定进程，将停止所有进程分析。|  
|[GC](../profiling/gc-vsperfcmd.md)[ **:** {**Allocation**`&#124;`**Lifetime**}]|收集 .NET 内存分配数据和对象生存期数据。 仅与 VSPerfCmdLaunch 选项一起使用。|  
  
### <a name="sampling-interval-options"></a>采样间隔选项  
 以下选项指定采样间隔的类型和持续时间。 默认值为 Timer。 还可以使用 Counter 选项将 CPU 计数器指定为间隔。 这些选项只能通过 Launch 或分析会话的第一个 Attach指定。  
  
|选项|描述|  
|------------|-----------------|  
|[PF](../profiling/pf.md)[ **:** _n_]|有关每个第 n 个页面错误的示例（默认值=10）。|  
|[Sys](../profiling/sys-vsperfcmd.md)[ **:** _n_]|有关每个第 n 个系统调用的示例（默认值=10）。|  
|[Timer](../profiling/timer.md)[ **:** _n_]|有关每个第 n 个处理器周期的示例（默认值=10000000）。|  
  
## <a name="service-component-and-kernel-mode-device-options"></a>服务组件和内核模式设备选项  
 以下 Admin 选项支持分析服务组件或内核模式设备驱动程序。 Admin 选项设置分析权限，并控制分析服务或设备驱动程序。  
  
 必须在使用管理凭据运行的命令提示符下执行 Admin 选项。  
  
|选项|描述|  
|------------|-----------------|  
|**管理员：安全性** \<**ALLOW&#124;DENY**>*Right*[ *right*]\<*User*&#124;*Group*>|允许或拒绝指定用户或组访问分析服务。<br /><br /> `Right` 可以是：<br /><br /> CrossSession - 允许用户访问此服务以执行跨会话分析。<br /><br /> SampleProfiling - 允许用户访问此驱动程序，以启用采样分析。 此外，用于在跟踪分析期间访问内核转换信息。<br /><br /> FullAccess - 允许用户访问 CrossSession 和 SampleProfiling。|  
|**Admin:Security, List**|列出分析服务的当前状态并列出用户权限。|  
|Admin: \<*Service*&#124;*Driver*>\<**START**&#124;**STOP**&#124;**INSTALL**&#124;**UNINSTALL**>|启动、停止、安装或卸载分析服务组件（服务）或内核模式设备驱动程序（驱动程序）。|  
|**管理员：** \<*Service*&#124;*Driver*>AutoStart\<**ON**&#124;**OFF**>|在重启后，启用或禁用自动启动分析服务（服务）或内核模式设备驱动程序（驱动程序）。|  
  
## <a name="vsperfcmd-driver"></a>VSPerfCmd /Driver  
 VSPerfCmd /Driver 选项现已过时。 将 VsPerfCmdAdmin**** 选项用于此功能。  
  
## <a name="see-also"></a>另请参阅  
 [VSInstr](../profiling/vsinstr.md)   
 [Vsperfmon.exe](../profiling/vsperfmon.md)   
 [VSPerfReport](../profiling/vsperfreport.md)
