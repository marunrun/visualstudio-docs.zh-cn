---
title: ProcessOn 和 ProcessOff | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d3dc6a7e-bc0f-48a6-a4ec-f386348bb296
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 62c16c2d578a38187b4a58958466597a5e4d297d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74778383"
---
# <a name="processon-and-processoff"></a>ProcessOn 和 ProcessOff
VSPerfCmd.exe **ProcessOff** 和 **ProcessOn** 子命令可暂停和继续对命令行分析会话中指定进程的分析。 **ProcessOff** 停止进程分析，而 **ProcessOn** 启动进程分析。

 大多数情况下，可指定 **ProcessOn** 或 **ProcessOff** 作为 VSPerfCmd.exe 命令行中唯一的选项，但它们也可与 **GlobalOn**、**GlobalOff**、**ThreadOn** 和 **ThreadOff** 子命令组合使用。

 **ProcessOn** 和 **ProcessOff** 子命令与控制命令行分析会话中所有进程的数据收集的 **GlobalOn** 和 **GlobalOff** 子命令交互，并与控制指定线程的数据收集的 **ThreadOn** 和 **ThreadOff** 子命令交互。

 **ProcessOff** 和 **ProcessOn** 子命令还影响探查器 API 函数所控制的进程启动/停止计数。

- **ProcessOff** 将进程启动/停止计数立即设置为 0，因此暂停分析。

- **ProcessOn** 将进程启动/停止计数立即设置为 1，因此继续分析。

  有关更多信息，请参阅[分析工具 API](../profiling/profiling-tools-apis.md)。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /{ProcessOff|ProcessOn}:PID [Options]

```

#### <a name="parameters"></a>参数
 `PID` 要启动或停止的进程的整数标识符。 Windows 任务管理器的“进程”选项卡上列出了进程 ID  。

## <a name="required-subcommands"></a>需要的子命令
 None

## <a name="valid-subcommands"></a>有效的子命令
 可以在包含以下子命令的命令行上指定 **ProcessOn** 和 **ProcessOff**。

 **Start:** `Method` 初始化命令行分析会话并设置指定的分析方法。

 **Launch：** `AppName` 启动指定的应用程序并开始使用采样方法进行分析。

 **Attach：** `PID` 开始分析指定的进程。

 GlobalOff&#124;GlobalOn 停止或启动对命令行分析会话中所有进程的分析   。

 {**ThreadOff**|**ThreadOn**} **:** `TID`停止或启动对指定线程的分析（仅限检测方法）。

## <a name="example"></a>示例
 在本示例中，**ProcessOff** 子命令用于收集应用程序启动的分析数据。

```cmd
; Initialize the profiler.
VSPerfCmd.exe /Start:Trace /Output:Instrument.vsp
; Start the instrumented application.
; Stop profiling the process after startup.
VSPerfCmd.exe /ProcessOff:12345
; Shut down the target application.
; Close the profiler.
VSPerfCmd /Shutdown

```

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)
