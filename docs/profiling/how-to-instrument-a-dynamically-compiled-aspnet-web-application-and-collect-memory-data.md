---
title: 探查器命令行：检测动态 ASP.NET 应用，获取内存数据
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 2cdd9903-39db-47e8-93dd-5e6a21bc3435
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: f784807a99c288663bee381bfc1e481dd9d5d8e4
ms.sourcegitcommit: 91c7f1b525e0c22d938bc4080ba4ceac2483474f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2019
ms.locfileid: "67031987"
---
# <a name="how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-memory-data-by-using-the-profiler-command-line"></a>如何：使用探查器命令行检测动态编译的 ASP.NET web 应用程序，并收集内存数据
本主题介绍如何使用检测分析方法和 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具为动态编译的 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序收集详细的 .NET 内存分配和对象生存期数据。

> [!NOTE]
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

 要从 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序收集性能数据，请修改目标应用程序的 web.config 文件，让 [VSInstr.exe](../profiling/vsinstr.md) 工具能够检测动态编译的应用程序文件  。 然后使用 [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) 工具来配置承载 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序的服务器并通过设置适当的环境变量启用 .NET 内存分析，然后重启计算机。

 若要收集数据，请启动探查器并运行目标应用程序。 在探查器附加到应用程序时，可以暂停并继续数据收集。收集适当的数据后，请关闭应用程序，关闭 Internet Information Services (IIS) 工作进程，然后关闭探查器。

 完成分析工作后，请将 web.config 文件和 Web 服务器还原到其原始状态  。

## <a name="configure-the-aspnet-web-application-and-the-web-server"></a>配置 ASP.NET Web 应用程序和 Web 服务器

#### <a name="to-configure-the-aspnet-web-application-and-the-web-server"></a>配置 ASP.NET Web 应用程序和 Web 服务器

1. 修改目标应用程序的 web.config 文件  。 请参阅[如何：将 web.Config 文件修改为检测和分析动态编译的 ASP.NET web 应用程序](../profiling/how-to-modify-web-config-files-to-instrument-dynamically-compiled-aspnet-apps.md)。

2. 在承载 Web 应用程序的计算机上打开命令提示符窗口。

3. 初始化分析环境变量。 类型：

     VSPerfClrEnv /globaltraceon 

     -或-

     VSPerfClrEnv /globaltracegclife 

    - /globaltracegc 启用对内存分配数据的收集  。

    - /globaltracegclife 启用对内存分配数据和对象生存期数据的收集  。

4. 重新启动计算机。

## <a name="run-the-profiling-session"></a>运行分析会话

#### <a name="to-profile-the-aspnet-web-application"></a>分析 ASP.NET Web 应用程序

1. 启动探查器。 类型：

    VSPerfCmd [/start](../profiling/start.md) :trace [/output](../profiling/output.md) : `OutputFile` [`Options`    ]

   - **/start:trace** 选项初始化探查器。

   - **/output:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置  。

     可以将以下任意选项与 **/start:trace** 选项一起使用。

   > [!NOTE]
   > **/user** 和 **/crosssession** 选项通常为 ASP.NET 应用程序所需选项。

   | 选项 | 说明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | 指定拥有 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程的帐户的可选域和用户名。 在进程以已登录用户外的用户身份运行时才需要此选项。 名称位于 Windows 任务管理器“进程”选项卡上的“用户名”列中   。 |
   | [/crosssession](../profiling/crosssession.md) | 启用其他会话中的进程分析。 如果应用程序在其他会话中运行，则需要此选项。 会话 ID 位于 Windows 任务管理器的“进程”选项卡上的“会话 ID”列中   。 可以将 **/CS** 指定为 **/crosssession** 的缩写。 |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | 在暂停数据收集的情况下启动探查器。 使用 [/globalon](../profiling/globalon-and-globaloff.md) 可恢复分析。 |
   | [/counter](../profiling/counter.md) **:** `Config` | 从 `Config` 中所指定的处理器性能计数器收集信息。 计数器信息将添加到在每个分析事件中收集的数据中。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | 指定要在分析期间收集的 Windows 性能计数器。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | 指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中  。 |

2. 以典型方式启动 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序。

## <a name="control-data-collection"></a>控制数据收集
 在目标应用程序运行时，可以通过使用 *VSPerfCmd.exe* 选项开始和停止向探查器数据文件写入数据，从而控制数据收集。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 以下选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|说明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|启动 ( **/threadon**) 或停止 ( **/threadoff**) 由线程 ID (`TID`) 指定的线程的数据收集。|

- 还可以使用 **VSPerfCmd.exe**[/mark](../profiling/mark.md) 选项将分析标记插入数据文件。 /mark 命令可添加标识符、时间戳和（可选）用户定义的文本字符串  。 标记可用于筛选探查器报告和数据视图中的数据。

## <a name="end-the-profiling-session"></a>结束分析会话
 要结束分析会话，请关闭目标 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序，停止 Internet Information Services (IIS) 以停止分析的进程，然后关闭探查器。 然后重启 IIS。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 关闭 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序。

2. 通过重置 Internet Information Services (IIS) 关闭 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程。 类型：

    **IISReset /stop**

3. 关闭探查器。 类型：

    VSPerfCmd [/shutdown](../profiling/shutdown.md) 

4. 重启 IIS。 类型：

    **IISReset /start**

## <a name="restore-the-application-and-computer-configuration"></a>还原应用程序和计算机配置
 完成全部分析后，请替换 web.config 文件，清除分析环境变量并重启计算机，以便将服务器和 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 应用程序还原到原始状态  。

#### <a name="to-restore-the-application-and-computer-configuration"></a>还原应用程序和计算机配置

1. 使用原始文件的副本替换 web.config 文件  。

2. （可选）。 清除分析环境变量。 类型：

     **VSPerfCmd /globaloff**

3. 重新启动计算机。

## <a name="see-also"></a>请参阅
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [.NET 内存数据视图](../profiling/dotnet-memory-data-views.md)
