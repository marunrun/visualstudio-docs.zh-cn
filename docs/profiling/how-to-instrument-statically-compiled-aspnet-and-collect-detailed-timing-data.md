---
title: 探查器命令行：检测静态 ASP.NET 应用，获取计时数据
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: b260ce68-76e6-4c3b-8062-3c00bd5cf7b8
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: 7d743dd854bd11449161c47cc896d0735849e1dd
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74778851"
---
# <a name="how-to-instrument-a-statically-compiled-aspnet-web-application-and-collect-detailed-timing-data-with-the-profiler-by-using-the-command-line"></a>如何：使用探查器命令行检测静态编译的 ASP.NET web 应用程序，并收集详细计时数据
本文介绍了如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具检测预编译的 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 组件或网站并收集详细计时数据。

> [!NOTE]
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。
>
> 若要将层交互数据添加到分析运行，需要使用命令行分析工具执行特定的步骤。 请参阅[收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md)。

 若要使用检测方法从 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 组件收集详细计时数据，请使用 [VSInstr.exe](../profiling/vsinstr.md) 工具生成组件的检测版本。 在托管组件的计算机上，将组件的非检测版本替换为检测版本。 然后使用 [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) 工具初始化全局分析环境变量并重新启动承载计算机。 然后启动探查器。

 在执行受检测组件时，会自动将计时数据收集到数据文件中。 在分析会话过程中可以暂停和恢复数据收集。

 要结束分析会话，请关闭承载该组件的 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程，然后直接关闭探查器。 在大多数情况下，建议在会话结束时清除分析环境变量。

## <a name="start-to-profile"></a>开始分析

#### <a name="to-instrument-an-aspnet-web-component-and-start-profiling"></a>检测 ASP.NET Web 组件并开始分析

1. 打开一个命令提示符窗口。

2. 使用 **VSInstr** 工具生成目标应用程序的受检测版本。 如有必要，将 ASP.NET 承载计算机上的应用程序二进制文件替换为已检测的二进制文件。

3. 初始化 .NET 分析环境变量。 在命令提示符窗口中，键入：

    **VSPerfClrEnv /globaltraceon**

4. 重新启动计算机。

5. 打开一个命令提示符窗口。 必要时，设置探查器工具路径。

6. 启动探查器。 类型：

    **VSPerfCmd /start:trace /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) **:trace** 选项初始化探查器。

   - [/output](../profiling/output.md) **:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置。

     可以将以下任意选项与 **/start:trace** 选项一起使用。

   > [!NOTE]
   > **/user** 和 **/crosssession** 选项通常为 ASP.NET 应用程序所需选项。

   | 选项 | 说明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | 指定拥有 ASP.NET 工作进程的帐户的域和用户名。 在进程以已登录用户外的用户身份运行时才需要此选项。 进程所有者在 Windows 任务管理器的“进程”选项卡上的“用户名”列中列出   。 |
   | [/crosssession](../profiling/crosssession.md) | 启用其他登录会话中的进程分析。 如果 ASP.NET 应用程序在其他会话中运行，则需要此选项。 会话标识符位于 Windows 任务管理器的“进程”选项卡上的“会话 ID”列中  。 可以将 **/CS** 指定为 **/crosssession** 的缩写。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | 指定要在分析期间收集的 Windows 性能计数器。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | 指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中  。 |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | 若要启动探查器而暂停数据收集，请将 **/globaloff** 选项添加到 **/start** 命令行。 使用 **/globalon** 可恢复分析。 |

7. 打开包含已检测的组件的网站。

## <a name="control-data-collection"></a>控制数据收集
 在目标应用程序运行时，可以通过使用 *VSPerfCmd.exe* 选项开始和停止向文件写入数据，从而控制数据收集。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 以下选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|说明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|启动 ( **/threadon**) 或停止 ( **/threadoff**) 由线程 ID (`TID`) 指定的线程的数据收集。|

## <a name="end-the-profiling-session"></a>结束分析会话
 要结束分析会话，请关闭 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用，然后使用 Internet Information Services (IIS) IISReset 命令来关闭 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程  。 调用 VSPerfCmd  [/shutdown](../profiling/shutdown.md) 选项关闭探查器和分析数据文件。

 VSPerfClrEnv /globaloff 命令会清除分析环境变量  。 必须重启计算机才能应用新的环境设置。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 关闭 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序。

2. 关闭 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程。 类型：

    **IISReset /stop**

3. 关闭探查器。 类型：

    **VSPerfCmd /shutdown**

4. （可选）。 清除分析环境变量。 类型：

    **VSPerfCmd /globaloff**

5. 重新启动计算机。

## <a name="see-also"></a>请参阅
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [检测方法数据视图](../profiling/instrumentation-method-data-views.md)
