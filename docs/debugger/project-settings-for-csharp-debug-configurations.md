---
title: C# 调试配置的项目设置 | Microsoft Docs
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62903952"
---
# <a name="project-settings-for--c-debug-configurations"></a>C# 调试配置的项目设置

可在项目属性页的[“调试”选项卡](#debug-tab)和[“生成”选项卡](#build-tab)中更改 C# 项目调试设置。

若要打开属性页，在“解决方案资源管理器”中选择项目，然后选择“属性”图标，或右键单击项目并选择“属性”  。

有关详细信息，请参见[调试和发布配置](how-to-set-debug-and-release-configurations.md)。

>[!IMPORTANT]
>这些设置不适用于 .NET Core、ASP.NET 或 UWP 应用。 若要为 UWP 应用配置调试设置，请参阅[启动 UWP 应用的调试会话](start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)。

## <a name="debug-tab"></a>“调试”选项卡

|设置|描述|
|-------------------------------------| - |
| **配置** | 设置用于生成应用的模式。 从下拉菜单中选择“活动(调试)”、“调试”、“发布”或“所有配置”。 |
| **启动操作** | 指定在调试配置中选择“开始”时的操作。<br />- “启动项目”是默认值，用于启动启动项目以供调试。 有关详细信息，请参阅[选择启动项目](/previous-versions/visualstudio/visual-studio-2010/0s590bew(v=vs.100))。<br />- **启动外部程序**启动并附加到不属于 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 项目的应用。 有关详细信息，请参阅[使用调试器附加到正在运行的进程](attach-to-running-processes-with-the-visual-studio-debugger.md)。<br />- **使用 URL 启动浏览器**让你可以调试 Web 应用。 |
| **启动选项** > **命令行参数** | 指定要调试的应用的命令行参数。 命令名称为“启动外部程序”中指定的应用名称。 |
| **启动选项** > **工作目录** | 指定要调试的应用的工作目录。 在 C# 中，默认情况下，工作目录为 \bin\debug。
| **启动选项** > **使用远程计算机**|对于远程调试，请选择此选项，然后输入远程调试目标的名称或 [Msvsmon 服务器名称](../debugger/remote-debugging.md)。 <br />应用在远程计算机上的位置由“生成”选项卡中的“输出路径”属性指定 。此位置必须是远程计算机上的共享目录。
| **调试器引擎** > **启用非托管代码调试** | 从托管应用调试对本机（非托管）Win32 代码的调用。 |
| **调试器引擎** > **启用 SQL Server 调试** | 调试 SQL Server 数据库对象。 |

## <a name="build-tab"></a>“生成”选项卡

|设置|描述|
|-------------|-----------------|
|**常规** > **条件编译符号**|定义 DEBUG 和 TRACE 常数（如果已选）。<br /><br /> 这些常数启用 [Debug](/dotnet/api/system.diagnostics.debug) 类和 [Trace](/dotnet/api/system.diagnostics.trace) 类的条件编译。 定义了这两个常数后，Debug 和 Trace 类方法将向[输出窗口](../ide/reference/output-window.md)生成输出。 如果没有这两个常数，则不编译 Debug 和 Trace 类方法，并且不生成任何输出。<br /><br />通常情况下，DEBUG 在生成的调试版本中定义，而不在发布版本中定义。 调试和发布版本中都定义了 TRACE。|
|**常规** > **优化代码**|除非 bug 仅在经过优化的代码中出现，否则对于“调试”生成，请取消选择此设置。 经过优化的代码更难调试，因为指令与源代码中的语句并不是直接对应关系。|
|**输出** > **输出路径**|通常设置为“bin\Debug”以进行调试。|
|“高级”按钮|有关高级调试选项的信息，请参阅[高级生成设置对话框 (C#)](../ide/reference/advanced-build-settings-dialog-box-csharp.md)。 符号的可移植格式 ( *.pdb*) 文件是 .NET Core 应用的最新跨平台格式。

## <a name="see-also"></a>请参阅
- [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)