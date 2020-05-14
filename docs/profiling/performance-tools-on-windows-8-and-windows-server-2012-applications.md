---
title: Windows 8 和 Windows Server 2012 应用上的性能工具
ms.date: 06/19/2017
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 3938e7dc1b3ec33c8a4cf74b6957067bbdfd6185
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74778422"
---
# <a name="performance-tools-on-windows-8-and-windows-server-2012-applications"></a>Windows 8 和 Windows Server 2012 应用程序上的性能工具

Windows 8 和 Windows Server 2012 中新增的增强安全功能需要对 Visual Studio 性能工具在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 本主题介绍针对 Windows 8 和 Windows Server 2012 平台上新增的性能工具所做的更改。

> [!NOTE]
> 其他受支持的 Windows 版本（Windows 7、Windows Server 2008 R2）的性能工具未更改。

## <a name="collect-data-on-uwp-apps-from-the-visual-studio-ide"></a>从 Visual Studio IDE 收集有关 UWP 应用的数据

分析在 JavaScript 和 HTML 5 中编写的 UWP 应用时，应收集 JavaScript 代码的检测数据。 分析在 Visual C++、Visual C# 或 Visual Basic 中编写的 UWP 应用或组件时，应收集本机代码和托管代码的采样数据。 可以在本地或远程计算机上分析应用。

分析 UWP 应用时不支持这些分析功能和选项：

- 使用采样方法分析 JavaScript 应用。
- 使用检测方法分析托管代码和本机代码。
- 并发分析
- .NET 内存分析
- 层交互分析 (TIP)
- 采样选项，如设置采样事件和计时间隔，或收集其他性能计数器数据。
- 检测选项，如收集性能和窗口计数器数据，或指定其他命令行选项。

有关分析 UWP 应用的详细信息，请参阅以下文章：

- [在本地计算机上运行 UWP 应用](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)
- [在远程计算机上运行 UWP 应用](../debugger/run-windows-store-apps-on-a-remote-machine.md)
- [首先了解分析工具](profiling-feature-tour.md)
- [JavaScript 内存](../profiling/javascript-memory.md)
- [分析本地计算机上的 UWP 应用中的 Visual C++、Visual C# 和 Visual Basic 代码](https://msdn.microsoft.com/2d0c939e-0bac-48c5-b727-46f6c6113060)
- [分析远程设备上的 UWP 应用中的 Visual C++、Visual C# 和 Visual Basic 代码](https://msdn.microsoft.com/b932a2be-11b0-40fd-b996-75c6b6a79d22)
- [分析 UWP 应用中的 Visual C++、Visual C# 和 Visual Basic 代码的性能数据](https://msdn.microsoft.com/5de4a413-d924-425f-afc4-e1ecfb0fca18)

## <a name="collect-data-on-apps-running-on-the-windows-8-desktop-or-on-windows-server-2012-from-the-visual-studio-ide"></a>从 Visual Studio IDE 收集有关在 Windows 8 桌面上或 Windows Server 2012 上运行的应用的数据

针对 Windows 8，使用检测方法进行分析并未更改。

使用采样方法时不支持层交互分析 (TIP)。

## <a name="collect-data-on-apps-running-on-the-windows-8-desktop-or-on-windows-server-2012-by-using-sampling-from-the-visual-studio-ide"></a>从 Visual Studio IDE 使用采样收集有关在 Windows 8 桌面上或 Windows Server 2012 上运行的应用的数据

使用采样方法分析 Windows 8 桌面应用程序或 Windows Server 2012 应用程序时不支持这些分析功能和选项。

- 层交互分析 (TIP)。 使用检测时支持收集 TIP 数据。

- 采样选项，如设置采样事件和计时间隔，或收集其他性能计数器数据。

## <a name="profile-from-the-command-line"></a>通过命令行进行分析

你使用两个命令行工具收集 Windows 8 和 Windows Server 2012 设备上的分析数据，这些设备包括未安装 Visual Studio 的设备：

|工具名称|说明|
|---------------|-----------------|
|[VSPerf](../profiling/vsperf.md)|从 UWP 应用收集分析数据，并从 Windows 8 桌面应用程序和 Windows Server 2012 应用程序收集采样分析数据。|
|[VSPerfCmd](../profiling/vsperfcmd.md)|从在 Windows 8 桌面和 Windows Server 2012 上运行的应用收集检测、并发和层交互分析数据。 从之前版本的 Windows 收集所有类型的分析数据。|

这两个工具都随 Visual Studio 一起安装以用于本地计算机。

若要分析未安装 Visual Studio 的设备上的应用程序，请执行以下操作之一：

- 从 [MSDN 网站](https://visualstudio.microsoft.com/#downloads+d-additional-software)上下载这些工具作为 Visual Studio 远程工具的一部分。

- 从你的 Visual Studio 计算机复制并运行独立探查器工具安装程序。 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 为远程计算机的操作系统 (x86/x64) 选择安装程序。

> [!NOTE]
> 若要收集 TIP 分析数据，必须从远程计算机上的 Visual Studio 计算机安装独立探查器。

当从命令行分析 Windows 8 和 Windows Server 2012 应用程序时不支持这些分析功能和选项：

- 通过将采样模式与 [VSPerfASPNetCmd](../profiling/vsperfaspnetcmd.md)一同使用，从 Windows 8 和 Windows Server 2012 Web 应用收集数据。

- 通过使用 VsPerfCmd.exe 收集采样数据。

- 采样选项，如设置采样事件和计时间隔，或收集其他性能计数器数据。

## <a name="collect-tier-interaction-tip-data"></a>收集层交互 (TIP) 数据

层交互分析提供有关多层应用程序函数执行时间的附加信息，这些应用程序通过 ADO.NET 服务与数据库进行通信。 仅针对同步函数调用收集数据。

**Visual Studio 版本**

可以使用任何版本的 Visual Studio 收集层交互分析数据。 但是，层交互分析数据只能在 Visual Studio Enterprise 中查看。

**Windows 8 和 Windows Server 2012**

1. 若要从在 Windows 8 桌面或 Windows Server 2012 上运行的应用中收集层交互数据，必须使用检测方法。

2. 不能收集 UWP 应用的层交互数据。

3. 您可以在所有分析方法中包含有关其他支持的 Windows 版本的层交互数据。

**性能向导和性能资源管理器**

必须从性能资源管理器将层交互数据收集选项添加到性能运行。 还必须将项目、可执行文件或网站添加到性能资源管理器的目标节点。 请参阅[收集层交互数据](../profiling/collecting-tier-interaction-data.md)。

**收集远程计算机上的 TIP 数据**

若要在远程计算机上收集层交互数据，必须从 Visual Studio 计算机的 %VSInstallDir%\Team Tools\Performance Tools\Setups 文件夹中将 vs**profiler\_\_Platform>** _Language>.exe 文件复制到远程计算机上并进行安装\<_ **\_** _\<_   。 不能使用[远程调试](../debugger/remote-debugging.md)下载包中的分析工具。

可以使用 [VSPerfCmd](../profiling/vsperfcmd.md) 或 [VSPerfASPNetCmd](../profiling/vsperfaspnetcmd.md) 收集分析数据。

**TIP 报告**

只能在 Visual Studio Enterprise 中查看层交互数据。 通过 [VSPerfReport](../profiling/vsperfreport.md) 生成的基于文件的层交互报告不可用。

## <a name="see-also"></a>另请参阅

[性能资源管理器](../profiling/performance-explorer.md)
[配置性能会话](../profiling/configuring-performance-sessions.md)
[通过命令行进行分析](../profiling/using-the-profiling-tools-from-the-command-line.md)
