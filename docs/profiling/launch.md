---
title: Launch | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f81bde5c-3394-4b79-a315-c2f6491689b3
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 9834c10c58fb343de0707fa0b805586a6cdebcb3
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74778604"
---
# <a name="launch"></a>启动
“Launch”选项使用采样方法启动探查器，还会启动指定的应用程序  。

 若要使用“Launch”选项，必须在“Start”选项中指定“Sample”方法    。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /Launch:AppName [Options]
```

#### <a name="parameters"></a>参数
 `AppName` 要启动的应用程序的名称。 支持当前目录的完整和部分路径。

## <a name="valid-options"></a>有效选项
 以下“VSPerfCmd”选项可以与单独命令行上的“启动”选项组合  。

 **Start:** `Method` 初始化命令行探查器会话并设置指定的分析方法。

 **GlobalOn** and **GlobalOff** 恢复 (GlobalOn) 或暂停 (GlobalOff) 分析，但不结束分析会话   。

 ProcessOn:  `PID` 和 ProcessOff  :`PID`恢复 (ProcessOn) 或暂停 (ProcessOff) 指定进程的分析   。

 **TargetCLR** 指定在分析会话中加载了多个版本的 .NET Framework 公共语言运行时 (CLR) 时，要分析的 .NET Framework CLR 版本。 默认情况下分析加载的第一个版本。

## <a name="exclusive-options"></a>独占选项
 以下选项只能与“Launch”选项一起使用  。

 **Console** 在新窗口中启动指定的命令行应用程序。

 **Args:** `ArgList` 指定要传递到应用程序的参数的列表。

 **LineOff** 禁用行级别分析数据的收集。

## <a name="sampling-options"></a>采样选项
 在 Launch 命令行中可以指定以下采样间隔选项之一  。 默认的采样间隔是 10,000,000 个处理器时钟周期。

 **Timer**[ **:** `Cycles`]**PF**[ **:** `Events`]**Sys**[ **:** `Events`]**Counter**[ **:** `Name`,`Reload`,`FriendlyName`]**GC**[:**allocation**&#124;**lifetime**] 指定采样间隔的数量和类型。

- Timer - 每 `Cycles` 个非暂停的处理器时钟周期采样一次  。 如果未指定 `Cycles`，则使用 10,000,000 个周期。

- PF - 每 `Events` 个页面错误采样一次  。 如果未指定 `Events`，则使用 10 个页面错误。

- Sys - 每 `Events` 次操作系统调用采样一次  。 如果未指定 `Events`，则使用 10 次系统调用。

- Counter - 每 `Reload` 个 `Name` 所指定的 CPU 性能计数器采样一次  。 或者，`FriendlyName` 可指定一个字符串，将其用作探查器报告中的列标头。

- GC - 收集 .NET 内存数据  。 默认情况 (allocation) 下，每次发生内存分配事件时都收集数据  。 如果指定 lifetime 参数，则每次发生垃圾回收事件时也收集数据  。

## <a name="example"></a>示例
 此示例演示如何使用 Launch 启动应用程序  。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Launch:TestApp.exe
```

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)
