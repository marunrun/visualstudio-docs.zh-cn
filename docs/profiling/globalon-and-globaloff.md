---
title: GlobalOn 和 GlobalOff | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 24b0ed68-d19e-473e-9af3-252c11d82bcf
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 518f41557809cdeaaae9f9e1ac79e3797a854395
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74776961"
---
# <a name="globalon-and-globaloff"></a>GlobalOn 和 GlobalOff
VSPerfCmd.exe 的“GlobalOff” 和“GlobalOn”选项可暂停和继续命令行分析会话中所有进程和线程的分析    。

 可以指定“GlobalOn”和“GlobalOff”作为 VSPerfCmd.exe 命令行中唯一的选项，也可在还包含“Start”、“Launch”或“Attach”选项的命令行中加入这两者       。

 “GlobalOn”  和“GlobalOff”  还可以与“ProcessOn”  、“ProcessOff”  、“ThreadOn”  和“ThreadOff”  选项组合使用。

 “GlobalOn”  和“GlobalOff”  选项与控制指定进程的数据收集的“ProcessOn”  和“ProcessOff”  选项交互，并与控制指定线程的数据收集的“ThreadOn”  和“ThreadOff”  选项交互。

 “GlobalOff”  和“GlobalOn”  选项还会影响探查器的 API 函数所操作的全局启动/停止计数。

- “GlobalOff”  将全局启动/停止计数立即设置为 0，从而暂停分析。

- “GlobalOn”  将全局启动/停止计数立即设置为 1，从而继续分析。

  有关详细信息，请参阅[分析工具 API](../profiling/profiling-tools-apis.md)。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /{GlobalOff|GlobalOn}

VSPerfCmd.exe /Start:Method /{GlobalOff|GlobalOn} [Options]

VSPerfCmd.exe {Launch:AppName|Attach:PID} /{GlobalOff|GlobalOn}[Options]
```

#### <a name="parameters"></a>参数
 无

## <a name="valid-options"></a>有效选项
 可以在还包含以下选项的命令行上指定“GlobalOn”  和“GlobalOff”  。

 **Start：** `Method` 初始化命令行探查器会话并设置指定的分析方法。

 **Launch：** `AppName` 启动指定的应用程序并开始使用采样方法进行分析。

 **Attach：** `PID` 开始分析指定的进程。

 {**ProcessOff**|**ProcessOn**} **:** `PID`停止或启动对指定进程的分析。

 {**ThreadOff**|**ThreadOn**} **:** `TID`停止或启动对指定进程的分析（仅限检测方法）。

## <a name="example"></a>示例
 在此示例中，“GlobalOff”  和“GlobalOn”  选项用于避免收集应用程序启动和关闭的分析数据。

```cmd
; Initialize the profiler with profiling stopped.
VSPerfCmd.exe /Start:Trace /Output:Instrument.vsp /GlobalOff
; Start an instrumented application and wait for it to warm up.
; Start profiling.
VSPerfCmd.exe /GlobalOn
; Exercise the application functionality that you want to profile.
; Stop profiling.
VSPerfCmd.exe /GlobalOff
; Shut down the target application.
; Close the profiler.
VSPerfCmd /Shutdown

```

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)
