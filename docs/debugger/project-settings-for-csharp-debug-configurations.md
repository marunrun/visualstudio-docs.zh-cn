---
title: 项目设置为C#调试配置 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/21/2018
ms.topic: reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debug configurations, C#
- project settings [Visual Studio], debug configurations
- debug builds, project settings
- projects [Visual Studio], debug configurations
- project configurations, debug
- debugging [C#], debugger settings
ms.assetid: e30ca810-66e9-4d6e-9cf6-9f285cd0b100
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: a5108e195e5df245c72436752316e8ee91781e7d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62903952"
---
# <a name="project-settings-for--c-debug-configurations"></a>C# 调试配置的项目设置

您可以更改C#项目中的调试设置[调试选项卡](#debug-tab)并[生成选项卡](#build-tab)的项目属性页。

若要打开属性页，选择中的项目**解决方案资源管理器**，然后选择**属性**图标，或右键单击该项目并选择**属性**。

有关详细信息，请参见[调试和发布配置](how-to-set-debug-and-release-configurations.md)。

>[!IMPORTANT]
>这些设置不适用于.NET Core、 ASP.NET 或 UWP 应用。 若要配置适用于 UWP 应用的调试设置，请参阅[启动调试会话的 UWP 应用](start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)。

## <a name="debug-tab"></a>“调试”选项卡

|设置|描述|
|-------------------------------------| - |
| **配置** | 设置用于生成应用程序的模式。 选择**活动 （调试）** ，**调试**，**版本**，或者**所有配置**从下拉列表。 |
| **启动操作** | 当选中指定的操作**启动**调试配置中。<br />- “启动项目”是默认值，用于启动启动项目以供调试  。 有关详细信息，请参阅[选择启动项目](/previous-versions/visualstudio/visual-studio-2010/0s590bew(v=vs.100))。<br />- **启动外部程序**启动，并将附加到的应用程序不是属于[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]项目。 有关详细信息，请参阅[将附加到正在运行调试器的进程](attach-to-running-processes-with-the-visual-studio-debugger.md)。<br />- **使用 URL 启动浏览器**使你能够调试 web 应用。 |
| **启动选项** > **命令行参数** | 指定应用程序正在调试的命令行参数。 该命令名是中指定的应用名称**启动外部程序**。 |
| **启动选项** > **工作目录** | 指定正在调试的应用程序的工作目录。 在C#，工作目录是 *\bin\debug*默认情况下。
| **启动选项** > **使用远程计算机**|对于远程调试，请选择此选项并输入为远程调试目标的名称或[Msvsmon 服务器名称](../debugger/remote-debugging.md)。 <br />指定远程计算机上的应用程序的位置**输出路径**上的属性**生成**选项卡。此位置必须是远程计算机上的共享目录。
| **调试器引擎** > **启用非托管的代码调试** | 调试从托管应用程序调用本机 （非托管） Win32 代码。 |
| **调试器引擎** > **启用 SQL Server 调试** | 调试 SQL Server 数据库对象。 |

## <a name="build-tab"></a>“生成”选项卡

|设置|描述|
|-------------|-----------------|
|**常规** > **条件编译符号**|如果选择，定义 DEBUG 和 TRACE 常量。<br /><br /> 这些常数启用 [Debug](/dotnet/api/system.diagnostics.debug) 类和 [Trace](/dotnet/api/system.diagnostics.trace) 类的条件编译。 定义了这两个常数后，Debug 和 Trace 类方法将向[输出窗口](../ide/reference/output-window.md)生成输出。 如果没有这两个常数，则不编译 Debug 和 Trace 类方法，并且不生成任何输出。<br /><br />通常情况下，调试生成的调试版本中定义和发布版本中未定义。 调试和发布版本中定义了跟踪。|
|**常规** > **优化代码**|除非仅在优化代码中出现 bug，否则请保留此设置，已取消选择对于调试版本。 优化的代码很难调试，因为说明执行操作不直接对应于在源代码中的语句。|
|**输出** > **输出路径**|通常设置为“bin\Debug”以进行调试  。|
|**高级**按钮|高级调试选项的信息，请参阅[高级的生成设置对话框 (C#)](../ide/reference/advanced-build-settings-dialog-box-csharp.md)。 符号的可移植格式 ( *.pdb*) 文件是.NET Core 应用程序的新跨平台格式。

## <a name="see-also"></a>请参阅
- [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)