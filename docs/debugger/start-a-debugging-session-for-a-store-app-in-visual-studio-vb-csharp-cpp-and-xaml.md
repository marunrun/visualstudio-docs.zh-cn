---
title: 启动调试会话的 UWP 应用 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/20/2018
ms.topic: conceptual
f1_keywords:
- VC.Project.IVCAppHostRemoteDebugPageObject.MachineName
- VC.Project.IVCAppHostRemoteDebugPageObject.BreakpointBehavior
- VC.Project.IVCAppHostLocalDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCAppHostTetheredDebugPageObject.DebuggerType
- VC.Project.IVCAppHostLocalDebugPageObject.BreakpointBehavior
- VC.Project.IVCAppHostRemoteDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostRemoteDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCAppHostLocalDebugPageObject.DebuggerType
- VC.Project.IVCAppHostSimulatorDebugPageObject.DebuggerType
- ImmersiveProjects.Properties.Debug
- VC.Project.IVCAppHostTetheredDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostSimulatorDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostSimulatorDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCAppHostLocalDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostLocalDebugPageObject.AllowLocalNetworkLoopback
- AppPackage.Properties.Debug
- VC.Project.IVCAppHostRemoteDebugPageObject.Authentication
- VC.Project.IVCAppHostRemoteDebugPageObject.DebuggerType
- VC.Project.IVCAppHostSimulatorDebugPageObject.BreakpointBehavior
- vs.debug.installedapppackagelauncher
- vs.debug.error.wwahost_scriptdebuggingdisabled
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 7c65662d054b8c3dd9e650fe088f7048cc3b4071
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62930052"
---
# <a name="start-a-debugging-session-for-a-uwp-app"></a>启动 UWP 应用的调试会话

本文介绍如何启动的通用 Windows 平台 (UWP) 应用的 Visual Studio 调试会话。 可以在 XAML 中编写的 UWP 应用和C++，XAML 和C#/Visual Basic。 若要开始调试 UWP 应用，请配置调试会话，并选择启动应用程序的方式。

::: moniker range=">=vs-2019"
> [!NOTE]
> 从 Visual Studio 2019 开始，不再支持适用于 HTML 和 JavaScript 的 UWP 应用。
::: moniker-end
::: moniker range="vs-2017"
在 Visual Studio 2017 中，大部分命令和本文中所示的选项也适用于 UWP 应用的 HTML 和 JavaScript。 命令是不同之间管理和C++应用程序，JavaScript 应用程序通常是相同的命令C++UWP 应用。
::: moniker-end

## <a name="BKMK_The_easy_way_to_start_debugging"></a>从 Visual Studio 工具栏中开始调试

若要配置和启动调试的最简单方法是从标准的 Visual Studio 工具栏。

![从工具栏进行调试](../debugger/media/vsrun_select_target_device.png)

1. 从**配置**上的下拉列表中**标准**工具栏中，选择**调试**。

1. 从**平台**下拉列表中，选择要为生成的目标平台。

1. 从绿色箭头旁边的下拉列表中，选择调试目标。 可以选择本地计算机、 设备直接连接，本地 Visual Studio 模拟器、 远程设备或仿真程序。

1. 若要开始调试，请选择绿色**启动**工具栏上或选择上的箭头**调试** > **开始调试**，或按**F5**.

   Visual Studio 生成并启动附有调试器的应用程序。

调试持续至抵达某个断点、 手动暂停执行，会发生未处理的异常，或应用结束为止。

### <a name="BKMK_Choose_the_deployment_target"></a> 部署目标选项

可以在 Visual Studio 工具栏中设置调试目标或项目的调试属性页。 选择下列选项之一：

|||
|-|-|
|**本地计算机**|在本地计算机上的当前会话中调试应用程序。|
|**模拟器**|调试 UWP 应用的 Visual Studio 模拟器中的应用程序。 模拟器是模拟设备功能，如触摸手势和设备旋转，可能不存在于本地计算机上的桌面窗口。 模拟器选项仅当应用程序的**目标平台最小值。版本**小于或等于在本地计算机上的操作系统。 有关详细信息，请参阅[在模拟器中的运行 UWP 应用](../debugger/run-windows-store-apps-in-the-simulator.md)。|
|**远程计算机**|调试通过网络或以太网电缆连接到本地计算机的设备上的应用程序。 适用于 Visual Studio 的远程工具必须是远程设备上安装并运行。 有关详细信息，请参阅[远程计算机上的运行 UWP 应用](../debugger/run-windows-store-apps-on-a-remote-machine.md)。|
|**设备**|调试连接了 USB 的设备上的应用。 设备必须为开发人员解锁且包含解锁屏幕。|
|**移动仿真程序**|启动模拟器名称中指定的仿真程序，部署该应用，并开始调试。 仿真程序是仅在启用了 HYPER-V 计算机上可用。|

## <a name="BKMK_Open_the_debugging_property_page_for_the_project"></a> 配置项目属性页中调试

若要配置其他调试选项，请使用项目的调试属性页。

**若要打开的调试属性：**

1. 在中**解决方案资源管理器**，选择的项目，然后选择**属性**图标，或右键单击该项目并选择**属性**。

1. 在左侧**属性**窗格：

   - 有关C#和 Visual Basic 应用程序，选择**调试**。

     ![C#和 Visual Basic 项目调试属性页](../debugger/media/dbg_csvb_debugpropertypage.png)

   - 有关C++应用程序中，选择**配置属性** > **调试**。

     ![C++UWP 应用调试属性页](../debugger/media/dbg_cpp_debugpropertypage.png)

### <a name="BKMK_Choose_the_debugger_to_use"></a> 选择要使用的调试器

有关C#和 Visual Basic 应用程序，Visual Studio 调试托管代码默认情况下。 您可以选择调试其他或其他代码类型。 您还可以设置**调试器类型**是项目的一部分的任何后台任务的值。

在C++应用程序，Visual Studio 默认情况下调试本机代码。 您可以选择调试特定类型的代码而不是，或调试本机代码。

**若要指定要调试的代码类型：**

- 有关C#和 Visual Basic 应用程序中，选择一个从以下调试器**应用程序类型**并**后台进程类型**下的下拉列表**调试器类型**上**调试**属性页。

- 有关C++应用中，选择一个从以下调试器**调试器类型**上的下拉列表**调试**属性页。

|||
|-|-|
|**仅限托管**|调试应用程序中的托管代码。 忽略 JavaScript 代码和本机 C/C++ 代码。|
|**仅限本机**|调试应用程序中的本机 C/C++ 代码。 忽略托管代码和 JavaScript 代码。|
|**混合(托管和本机)**|调试应用程序中的本机 C/C++ 代码和托管代码。 忽略 JavaScript 代码。 在C++项目中，此选项称为**托管和本机**。|
|**脚本**|调试应用程序中的 JavaScript 代码。 忽略托管代码和本机代码。|
|**带脚本的本机**|调试本机 C /C++代码和应用程序中的 JavaScript 代码。 忽略托管的代码。 可在C++项目或后台任务仅。|
|**仅限 GPU (C++ AMP)**|调试在图形处理单元 (GPU) 上运行的本机 C++ 代码。 可在C++仅适用于项目。|

### <a name="BKMK__Optional__Disable_network_loopbacks"></a> 禁用网络环回 （可选）

 为了安全，标准方式安装的 UWP 应用不能进行网络调用安装的设备。 Visual Studio 豁免默认情况下部署此规则从应用程序，因此可以测试一台计算机上的通信过程。 在发布应用之前，应测试应用程序，无例外。

**若要移除网络环回例外，请执行以下操作：**

- 有关C#和 Visual Basic 应用程序，请取消选中**允许本地网络环回**下的复选框**启动选项**上**调试**属性页。

- 视觉对象C++应用程序中，选择**否**从**允许本地网络 Loopback**上的下拉列表**调试**属性页。

### <a name="BKMK__Optional__Reinstall_the_app_when_you_start_debugging"></a> 重新安装该应用，在开始调试时 （可选）
 若要诊断安装问题C#或 Visual Basic 应用程序，选择**卸载并重新安装我的程序包**上**调试**属性页。 在开始调试时，此选项将重新创建原始安装。 此选项不适用于C++项目。

### <a name="BKMK__Optional__Disable_authentication_requirement_to_start_the_remote_debugger"></a> 设置远程调试的身份验证选项

默认情况下，必须提供 Windows 凭据来运行远程调试器时选择**远程计算机**作为部署目标。 您可以更改身份验证要求。

**通用 （未加密的协议）** 身份验证模式是为 IoT、 Xbox 和 HoloLens 设备和创建者的更新或更高版本的 Windows 10 电脑。

**若要更改身份验证方法：**

- 有关C#和 Visual Basic 应用程序上**调试**属性页上，选择**远程计算机**作为**目标设备**。 然后，选择**无**或**通用 （未加密的协议）** 有关**身份验证模式**。

- 有关C++应用程序中，选择**远程计算机**下**要启动的调试器**上**调试**属性页。 然后，选择**无身份验证**或**通用 （未加密的协议）** 有关**身份验证类型**。

> [!CAUTION]
> 没有任何网络安全中运行远程调试器时**无**或**通用 （未加密的协议）** 模式。 选择仅在你的受信任的网络上的以下模式确保不在会受到恶意代码或恶意流量。

## <a name="BKMK_Start_the_debugging_session"></a> 调试启动选项

当选择**调试** > **开始调试**或按**F5**，Visual Studio 启动附带调试器的应用程序。 持续执行至抵达某个断点、手动暂停执行、发生无法处理的异常或应用程序结束为止。

### <a name="BKMK_Start_debugging__F5__but_delay_the_app_start"></a> 启动但延迟应用启动调试

默认情况下，Visual Studio 开始调试后，将立即启动应用。 此外可以设置应用程序以在调试模式下运行，但启动在调试器外部应用程序。 例如，你可能想要调试从 Windows 应用程序启动**启动**菜单中或调试应用程序中的后台进程。 如果选择此选项，应用将在启动调试器中启动。

**若要禁用自动应用程序启动：**

- 有关C#和 Visual Basic 应用程序，选择**不启动，但在启动时调试我的代码**下**启动选项**上**调试**属性页。

- 有关C++应用程序中，选择**否**从**启动应用程序**上的下拉列表**调试**属性页。

有关调试后台任务的详细信息，请参阅[触发器挂起、 继续和后台事件适用于 UWP 应用](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)。

### <a name="BKMK_Start_an_installed_app_in_the_debugger"></a> 调试已安装或正在运行 UWP 应用

可以使用**调试安装的应用程序包**调试已安装或运行在本地或远程设备上的 UWP 应用。 应用程序可能已安装从 Microsoft Store 中，也可能不是 Visual Studio 项目。 例如，应用可能具有不使用 Visual Studio 的自定义生成系统。

您可以立即启动已安装的应用，或您可以将其设置为使用另一种方法启动时在调试器中运行。 有关详细信息，请参阅[触发器挂起、 继续和后台事件适用于 UWP 应用)](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)。

若要在调试器中启动已安装或正在运行 UWP 应用，请选择**调试** > **其他调试目标** > **调试安装的应用程序包**。 有关详细说明，请参阅[调试安装的应用包](../debugger/debug-installed-app-package.md)。

### <a name="BKMK_Attach_the_debugger_to_a_running_app_"></a> 将调试器附加到正在运行的 Windows 8.x 应用

若要将调试器附加到 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 应用程序，必须使用可调式包管理器将应用程序设置为以调试模式运行。 可调式包管理器与远程工具安装用于 Visual Studio。

1. 用于 Visual Studio 安装的应用在设备上安装远程工具。 有关详细信息，请参阅[安装远程工具](../debugger/remote-debugging.md)。

1. 在 Windows 中**启动**屏幕上，搜索并开始**可调式包管理器**。

   随后显示 PowerShell 窗口，该窗口针对 AppxDebug cmdlet 进行了正确的配置。

1. 指定应用的 PackageFullName 标识符。

   1. 若要查看包含 PackageFullName 的所有应用的列表，请键入`Get-AppxPackage`在 PowerShell 提示符下。

   1. 在 PowerShell 提示符下输入`Enable-AppxDebug <PackageFullName>`，其中\<PackageFullName > 是应用的 PackageFullName 标识符。

1. 选择“调试” > “附加到进程”。

1. 在中**附加到进程**对话框框中，指定在远程设备**连接目标**框。

   可以输入设备名称，从下拉列表中选择它**连接目标**框中，或选择**查找**若要查找中的设备**远程连接**对话框。

1. 若要指定想要调试下, 一步的代码类型**将附加到**框中，选择**选择**。

1. 在中**选择代码类型**对话框框中，选择：
   - **自动确定要调试的代码类型**，或
   - **调试以下代码类型**，然后从列表中选择一个或多个代码类型。

1. 在中**可用进程**列表中，选择要调试的应用程序进程。

1. 选择“附加”。

 Visual Studio 将调试器附加到该进程。 持续执行至抵达某个断点、手动暂停执行、发生无法处理的异常或应用程序结束为止。

::: moniker range="vs-2017"
> [!NOTE]
> JavaScript 应用使用“wwahost.exe”进程的实例运行。 如果多个 JavaScript 应用正在运行，您需要知道您的应用程序的数字进程 id (PID) *wwahost.exe*要附加到该进程。
>
> 若要将附加到 JavaScript 应用程序的最简单方法是关闭所有其他 JavaScript 应用。 或者，可以记下运行的 Pid *wwahost.exe*进程在 Windows 任务管理器之前启动应用。 当启动应用，其*wwahost.exe* PID 将不同于先前记下的一个。
::: moniker-end

## <a name="see-also"></a>请参阅
- [在 Visual Studio 中调试应用](/visualstudio/debugger/debugging-windows-store-and-windows-universal-apps)