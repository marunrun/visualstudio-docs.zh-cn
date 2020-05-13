---
title: ThreadOn 和 ThreadOff | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 5cd5a695-0a14-484a-8952-ed47e13d8e92
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 906629eb24f6be097f3e24dfca3e6a231f42357f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74778149"
---
# <a name="threadon-and-threadoff"></a>ThreadOn 和 ThreadOff
VSPerfCmd.exe ThreadOff 和 ThreadOn 子命令只能在使用检测方法的命令行分析会话中使用    。 **ThreadOff** 和 **ThreadOn** 可暂停和继续指定线程的分析。 **ThreadOff** 停止线程分析，而 **ThreadOn** 启动线程分析。

 大多数情况下，可指定 ThreadOn 或 ThreadOff 作为 VSPerfCmd.exe 命令行中唯一的选项，但它们也可与 GlobalOn、GlobalOff、ProcessOn 和 ProcessOff 子命令组合使用        。

 **ThreadOn** 和 **ThreadOff** 子命令与控制命令行分析会话中所有进程的数据收集的 **GlobalOn** 和 **GlobalOff** 子命令交互，并与控制指定进程的数据收集的 **ProcessOn** 和 **ProcessOff** 子命令交互。

 **ThreadOff** 和 **ThreadOn** 子命令还影响探查器 API 函数所控制的线程启动/停止计数。

- **ThreadOff** 将线程启动/停止计数立即设置为 0，从而暂停分析。

- **ThreadOn** 将线程启动/停止计数立即设置为 1，从而继续分析。

  有关详细信息，请参阅[分析工具 API](../profiling/profiling-tools-apis.md)。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /{ThreadOff|ThreadOn}:TID [Options]

```

#### <a name="parameters"></a>参数
 `TID` 要启动或停止的线程的整数标识符。

## <a name="valid-options"></a>有效选项
 可以在包含以下子命令的命令行上指定 **ThreadOn** 和 **ThreadOff**。

 **Start:** `Method` 初始化命令行分析会话并设置指定的分析方法。

 GlobalOff&#124;GlobalOn 停止或启动对命令行分析会话中所有进程的分析   。

 {**ProcessOff**|**ProcessOn**} **:** `TID`停止或启动对指定进程的分析。

## <a name="example"></a>示例
 在本示例中，**ThreadOff** 子命令用于停止收集分析数据，以便仅收集应用程序启动数据。

```cmd
; Initialize the profiler.
VSPerfCmd.exe /Start:Trace /Output:Instrument.vsp
; Start the instrumented application.
; Stop profiling the thread after startup.
VSPerfCmd.exe /ThreadOff:12345
; Shut down the target application.
; Close the profiler.
VSPerfCmd /Shutdown

```

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)
