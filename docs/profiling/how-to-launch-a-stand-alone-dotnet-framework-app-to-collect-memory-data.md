---
title: 探查器命令行：打开客户端 .NET Framework 应用，获取内存数据
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 3bc53041-91b7-4ad0-8413-f8bf2c4b3f5e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 1a1d08656ea4234f277265c81b1bef4275de7625
ms.sourcegitcommit: 91c7f1b525e0c22d938bc4080ba4ceac2483474f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2019
ms.locfileid: "67032951"
---
# <a name="how-to-launch-a-stand-alone-net-framework-application-with-the-profiler-to-collect-memory-data-by-using-the-command-line"></a>如何：使用探查器启动独立 .NET Framework 应用程序，以使用命令行收集内存数据
本主题介绍如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具启动 .NET Framework 独立（客户端）应用程序以及收集内存数据。

 分析会话包括三部分：

- 使用探查器启动应用程序。

- 收集分析数据。

- 结束分析会话。

> [!NOTE]
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

## <a name="start-the-application-with-the-profiler"></a>用探查器启动应用程序
 若要使用探查器来启动目标应用程序，请使用 **VSPerfCmd.exe/start** 和 **/launch** 选项来初始化探查器并启动应用程序。 可以在一个命令行中指定 **/start** 和 **/launch** 及其各自的选项。

 还可以添加 **/globaloff** 选项，以在目标应用程序启动时暂停数据收集。 然后可使用 **/globalon** 开始收集数据。

#### <a name="to-start-an-application-by-using-the-profiler"></a>用探查器启动应用程序

1. 打开一个命令提示符窗口。

2. 启动探查器。 类型：

    **VSPerfCmd /start:sample /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) **:sample** 选项初始化探查器。

   - [/output](../profiling/output.md) **:** `OutputFile` 选项需要与 **/start** 一起使用。 `OutputFile` 指定分析数据 (.vsp) 文件的名称和位置。

     可以将以下任意选项与 **/start:sample** 选项一起使用。

   | 选项 | 说明 |
   | - | - |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | 指定要在分析期间收集的 Windows 性能计数器。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | 仅与 **/wincounter** 一起使用。 指定两次 Windows 性能计数器收集事件相隔的毫秒数。 默认值为 500 毫秒。 |

3. 启动目标应用程序。 类型：

    **VSPerfCmd**  [/launch](../profiling/launch.md) **:** `appName` **/gc:** {**allocation**&#124;**lifetime**}[`Options`]

   - 需要 [/gc](../profiling/gc-vsperfcmd.md) **:** `Keyword` 选项才能收集 .NET Framework 内存数据。 keyword 参数指定是收集内存分配数据，还是同时收集内存分配数据和对象生存期数据。

     |关键字|说明|
     |-------------|-----------------|
     |**allocation**|仅收集内存分配数据。|
     |**lifetime**|同时收集内存分配数据和对象生存期数据。|

     可以将以下任意选项与 **/launch** 选项一起使用。

   |选项|说明|
   |------------|-----------------|
   |[/args](../profiling/args.md) **:** `Arguments`|指定一个字符串，其中包含要传递给目标应用程序的命令行参数。|
   |[/console](../profiling/console.md)|在另一个窗口中启动目标命令行应用程序。|
   |[/events](../profiling/events-vsperfcmd.md) **:** `Config`|指定要在分析期间收集的 Windows 事件跟踪 (ETW) 事件。 ETW 事件收集在单独的 (.etl) 文件中。|
   |[/targetclr](../profiling/targetclr.md) **:** `Version`|指定应用程序中加载公共语言运行时 (CLR) 的多个版本时要分析的运行时的版本。|

## <a name="control-data-collection"></a>控制数据收集
 在目标应用程序运行时，可以通过使用 *VSPerfCmd.exe* 选项开始和停止向文件写入数据，从而控制数据收集。 通过控制数据收集，可以针对程序执行的特定部分（如启动或关闭应用程序）进行数据收集。

#### <a name="to-start-and-stop-data-collection"></a>启动和停止数据收集

- 以下选项对可启动和停止数据收集。 在单独的命令行上指定每个选项。 可多次打开和关闭数据收集。

    |选项|说明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|启动 ( **/globalon**) 或停止 ( **/globaloff**) 所有进程的数据收集。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [processoff](../profiling/processon-and-processoff.md) **:** `PID`|启动 ( **/processon**) 或停止 ( **/processoff**) 由进程 ID (`PID`) 指定的进程的数据收集。|
    |[/attach](../profiling/attach.md) **:** `PID` [/detach](../profiling/detach.md)|**/attach** 将启动由 `PID`（进程 ID）指定的进程的数据收集。 **/detach** 将停止所有进程的数据收集。|

- 还可以使用 **VSPerfCmd.exe**[/mark](../profiling/mark.md) 选项将分析标记插入数据文件。 **/mark**命令可添加标识符、时间戳和（可选）用户定义的文本字符串。 标记可用于筛选数据。

## <a name="end-the-profiling-session"></a>结束分析会话
 若要结束分析会话，必须将探查器与所有被分析进程分离，并且必须显式关闭探查器。 可通过关闭应用程序或调用 **VSPerfCmd /detach** 选项从使用采样方法分析的应用程序分离探查器。 然后，可以调用 **VSPerfCmd /shutdown** 选项关闭探查器和分析数据文件。 **VSPerfClrEnv /off** 命令会清除分析环境变量。

#### <a name="to-end-a-profiling-session"></a>结束分析会话

1. 执行下列步骤之一，从目标应用程序分离探查器：

    - 关闭目标应用程序。

         -或-

    - 键入 **VSPerfCmd /detach**

2. 关闭探查器。 类型：

     **VSPerfCmd** [/shutdown](../profiling/shutdown.md)

## <a name="see-also"></a>请参阅
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [.NET 内存数据视图](../profiling/dotnet-memory-data-views.md)