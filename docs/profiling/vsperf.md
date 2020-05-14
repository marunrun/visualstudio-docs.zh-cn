---
title: VSPerf | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: b5854e62-279e-4850-bfeb-0c6ef82f4805
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 051c983920ddc80909d721e569c5efb5ecd33a7c
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779930"
---
# <a name="vsperf"></a>VSPerf
使用 **VsPerf** 命令行工具可以：

1. 在设备上未安装 Visual Studio 时，从命令行分析 UWP 应用。

2. 使用采样分析方法分析 Windows 8 桌面应用程序和 Windows Server 2012 应用程序。

   有关分析选项的详细信息，请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

## <a name="uwp-apps-only"></a>仅 UWP 应用
 这些选项仅适用于 UWP 应用。

|||
|-|-|
|**/app:{AppName}**|启动探查器，然后等待指定的应用从“开始”菜单中启动。<br /><br /> 运行 `vsperf /listapps` 以查看应用名称和已安装应用的 PackageFullName。|
|**/package:{PackageFullName}**|启动探查器，然后等待指定的应用从“开始”菜单中启动。<br /><br /> 运行 `vsperf /listapps` 以查看应用名称和已安装应用的 PackageFullName。|
|**/js**|分析 JavaScript 应用所必需的。<br /><br /> 从 JavaScript 应用中收集性能数据。<br /><br /> 仅与 /package 或 /attach 一起使用。|
|**/noclr**|可选。 不收集 CLR 数据。<br /><br /> 仅与 /package 或 /attach 一起使用。<br /><br /> 优化，不会解析任何托管符号。|
|**/listapps**|列出已安装的应用名称和 PackageFullNames。|

## <a name="windows-8-desktop-applications-and-windows-server-2012-applications-only"></a>仅限 Windows 8 桌面应用程序和 Windows Server 2012 应用程序
 这些选项不适用于 UWP 应用。

|||
|-|-|
|**/launch:{Executable}**|启动并开始分析指定的可执行文件。|
|**/args:{ExecutableArguments}**|指定要传递 **/launch** 目标的命令行参数。|
|**/console**|在新的命令窗口中运行 **/launch** 目标。|

## <a name="all-applications"></a>所有应用程序
 这些选项适用于任何 Windows 8 或 Windows Server 2012 应用程序。

|||
|-|-|
|**/attach:{PID&#124;ProcessName}[,PID&#124;ProcessName]...**|从指定的进程收集数据。<br /><br /> 使用任务管理器查看正在运行的应用的进程 ID (PID) 和进程名称。|
|**/file:{ReportName}**|可选。 指定输出文件（将覆盖现有文件）。<br /><br /> 仅与 /package 或 /attach 一起使用。|
|**/pause**|暂停数据收集。|
|**/resume**|恢复数据收集。|
|**/stop**|停止数据收集并终止目标进程。|
|**/detach**|停止数据收集，但允许目标进程继续运行。|
|**/status**|显示探查器状态。|

## <a name="see-also"></a>另请参阅
- [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)
- [通过命令行分析](../profiling/using-the-profiling-tools-from-the-command-line.md)
