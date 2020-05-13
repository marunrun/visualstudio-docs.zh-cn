---
title: Attach | Microsoft 文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 79614283-6733-4592-a53a-d428052271ad
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 634169607a7d581de1b1332d78e8d5abde1a722e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74773734"
---
# <a name="attach"></a>Attach
VSPerfCmd.exe“Attach”选项开始对进程 ID (PID) 指定的运行过程进行样本分析   。

 若要使用“Attach”  选项，必须在“Start”选项中指定“Sample”  方法。

> [!NOTE]
> 如果已使用“Crosssession”  选项指定“Start”  选项，则对 VSPerfCmd /Attach  或 VSPerfCmd /Detach  的任何调用也必须指定“Crosssession”  。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /Attach:ProcessID [Options]
```

#### <a name="parameters"></a>参数
 `ProcessID` 正在运行的进程的进程 ID (PID)。 正在运行的进程的 PID 列在 Windows 任务管理器的“进程”选项卡上。

## <a name="valid-options"></a>有效选项
 以下“VSPerfCmd”  选项可以与单独命令行上的“Attach”  选项组合。

 **Crosssession** 允许分析登录会话以外的会话中的应用程序。 如果同时指定“Start”  选项和“Crosssession”  选项，则为必需。

 **Start:** `Method` 初始化命令行探查器会话并设置指定的分析方法。

 **TargetCLR** 指定在分析会话中加载了多个版本的 .NET Framework 公共语言运行时 (CLR) 时，要分析的 .NET Framework CLR 版本。 默认情况下分析加载的第一个版本。

 **GlobalOn GlobalOff** 恢复 (GlobalOn) 或暂停 (GlobalOff) 分析，但不结束分析会话   。

 **ProcessOn：** `PID` **ProcessOff:** `PID` 恢复 (ProcessOn) 或暂停 (ProcessOff) 指定进程的分析   。

## <a name="interval-options"></a>间隔选项
 在 Attach 命令行中可以指定以下采样间隔选项之一。 默认的采样间隔是 10,000,000 个处理器时钟周期。

 **Timer**[ **:** `Cycles`]**PF**[ **:** `Events`]**Sys**[<strong>:</strong>Events]**Counter**[ **:** `Name`,`Reload`,`FriendlyName`] 指定采样间隔的数量和类型。

- Timer  - 每 `Cycles` 个处理器时钟周期采样一次。 如果未指定 `Cycles`，则使用 10,000,000 个周期。

- PF - 每 `Events` 个页面错误采样一次  。 如果未指定 `Events`，则使用 10 个页面错误。

- Sys - 每 `Events` 次操作系统调用采样一次  。 如果未指定 `Events`，则使用 10 次系统调用。

- Counter - 每 `Reload` 个 `Name` 所指定的 CPU 性能计数器采样一次  。 或者，`FriendlyName` 可指定一个字符串，将其用作探查器报告中的列标头。

## <a name="example"></a>示例
 此示例演示如何附加到进程 ID 为 12345 的正在运行的应用程序实例。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Attach:12345
```

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)
