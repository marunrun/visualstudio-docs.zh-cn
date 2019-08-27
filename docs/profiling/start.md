---
title: Start | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: b85d0fe9-f67a-4b7c-8d48-7eecf3f2dfe9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e85c589866aba54e856afb066cec253c7057aaad
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62979674"
---
# <a name="start"></a>Start
Start 选项是一个 VSPerfCmd.exe 选项，可将探查器初始化为指定分析方法。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /Start:Method /Output:FileName [Options]
```

#### <a name="parameters"></a>参数
 `Method` 必须是以下关键字之一：

- **TRACE** - 指定检测方法。

- **SAMPLE** - 指定采样方法。

- **COVERAGE** - 指定代码覆盖率。

- **CONCURRENCY** - 指定资源争用方法。

## <a name="required-options"></a>必需选项
 在命令行上指定 **Start** 时，必须指定 **Output** 选项。

 **输出：**`filename` 指定输出文件名。

## <a name="exclusive-options"></a>独占选项
 以下选项只能在命令行上与 **Start** 选项一起使用。

 **CrossSession**&#124;**CS** 启用跨进程分析。 同时支持选项名 **CrossSession** 和 **CS**。

 **User:**[`domain\`]`username` 使客户端可以用指定帐户访问监视器。

 **WinCounter:** `Path` [**Automark**:`n`] WinCounter 指定要作为标记包含在分析数据文件中的 Windows 性能计数器。 **AutoMark** 以毫秒为单位指定数据文件的收集之间的间隔。

## <a name="invalid-options"></a>无效选项
 以下选项不能在命令行上与 **Start** 选项一起使用。

 **Status** Status 适用于用于被分析的进程。 它列出进程和线程及其当前分析状态 (On/Off)。 例如，如果某个进程已停止，则 **Status** 不会在报告中对此进行指示。 **Status** 会显示该进程是否进行分析。

 **Shutdown**[**:**`Timeout`] 关闭探查器。

## <a name="example"></a>示例
 以下示例演示如何使用 VSPerfCmd.exe Start 选项来初始化探查器。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Launch:TestApp.exe
```

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)