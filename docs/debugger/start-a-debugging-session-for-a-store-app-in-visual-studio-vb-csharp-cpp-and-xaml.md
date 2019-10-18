---
title: 为 UWP 应用启动调试会话 |Microsoft Docs
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
ms.openlocfilehash: c4504dda362c8a50f33168a12839e894a14316d7
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72436014"
---
# <a name="start-a-debugging-session-for-a-uwp-app"></a>启动 UWP 应用的调试会话

本文介绍如何启动通用 Windows 平台（UWP）应用的 Visual Studio 调试会话。 UWP 应用可以编写为 XAML C++、xaml 和C#/Visual Basic。 若要开始调试 UWP 应用，请配置调试会话，然后选择启动应用的方式。

::: moniker range=">=vs-2019"
> [!NOTE]
> 从 Visual Studio 2019 开始，不再支持用于 HTML 和 JavaScript 的 UWP 应用。
::: moniker-end
::: moniker range="vs-2017"
在 Visual Studio 2017 中，本文中所示的大部分命令和选项还适用于 HTML 和 JavaScript 的 UWP 应用。 托管应用和C++应用中的命令不同，JavaScript 应用通常与C++ UWP 应用的命令相同。
::: moniker-end

## <a name="BKMK_The_easy_way_to_start_debugging"></a>从 Visual Studio 工具栏启动调试

配置和启动调试的最简单方法是从标准 Visual Studio 工具栏中进行配置。

![从工具栏调试](../debugger/media/vsrun_select_target_device.png)

1. 从 "**标准**" 工具栏上的 "**配置**" 下拉列表中，选择 "**调试**"。

1. 从 "**平台**" 下拉列表中，选择要为其生成的目标平台。

1. 从绿色箭头旁边的下拉列表中，选择调试目标。 可以选择本地计算机、直接连接的设备、本地 Visual Studio 模拟器、远程设备或仿真程序。

1. 若要开始调试，请选择工具栏上的绿色**启动**箭头，或选择 "**调试**"  >  "**开始调试**"，或按**F5**。

   Visual Studio 生成并启动附有调试器的应用程序。

调试将继续，直到到达断点、手动挂起执行、发生未处理的异常或应用程序结束。

### <a name="BKMK_Choose_the_deployment_target"></a>部署目标选项

您可以在 Visual Studio 工具栏或项目的 "调试" 属性页中设置调试目标。 选择下列选项之一：

|||
|-|-|
|**本地计算机**|在本地计算机上的当前会话中调试应用程序。|
|**模拟器**|在适用于 UWP 应用的 Visual Studio 模拟器中调试应用。 模拟器是一个桌面窗口，用于模拟本地计算机上可能不存在的设备功能，如触摸手势和设备旋转。 仅当应用的**目标平台最小版本**低于或等于本地计算机上的操作系统时，模拟器选项才可用。 有关详细信息，请参阅[在模拟器中运行 UWP 应用](../debugger/run-windows-store-apps-in-the-simulator.md)。|
|**远程计算机**|在通过网络或以太网电缆连接到本地计算机的设备上调试应用程序。 必须在远程设备上安装并运行 Visual Studio 远程工具。 有关详细信息，请参阅[在远程计算机上运行 UWP 应用](../debugger/run-windows-store-apps-on-a-remote-machine.md)。|
|**设备**|在 USB 连接的设备上调试应用程序。 设备必须已进行开发人员解除锁定，并使屏幕处于解锁状态。|
|**移动模拟器**|启动在模拟器名称中指定的模拟器，部署应用程序，然后开始调试。 仿真器仅在启用 Hyper-v 的计算机上可用。|

## <a name="BKMK_Open_the_debugging_property_page_for_the_project"></a>在项目属性页中配置调试

若要配置其他调试选项，请使用项目的 "调试" 属性页。

**打开 "调试" 属性：**

1. 在**解决方案资源管理器**中，选择该项目，然后选择 "**属性**" 图标，或右键单击该项目并选择 "**属性**"。

1. 在 "**属性**" 窗格的左侧：

   - 对于C#和 Visual Basic 应用，请选择 "**调试**"。

     ![C#和 Visual Basic 项目调试属性页](../debugger/media/dbg_csvb_debugpropertypage.png)

   - 对于C++应用，请选择 "**配置属性**"  > **调试**。

     ![C++UWP 应用调试属性页](../debugger/media/dbg_cpp_debugpropertypage.png)

### <a name="BKMK_Choose_the_debugger_to_use"></a> 选择要使用的调试器

对于C#和 Visual Basic 应用，默认情况下，Visual Studio 调试托管代码。 你可以选择调试其他或其他代码类型。 还可以为作为项目的一部分的任何后台任务设置**调试器类型**值。

在C++应用中，默认情况下，Visual Studio 调试本机代码。 您可以选择调试特定类型的代码而不是本机代码，而不是本机代码。

**指定要调试的代码类型：**

- 对于C#和 Visual Basic 应用，从 "**调试**" 属性页上 "**调试器类型**" 下的 "**应用程序类型**" 和 "**后台进程类型**" 下拉列表中选择以下调试器之一。

- 对于C++应用，从 "**调试**" 属性页上的 "**调试器类型**" 下拉列表中选择以下调试器之一。

|||
|-|-|
|**仅限托管**|调试应用程序中的托管代码。 忽略 JavaScript 代码和本机 C/C++ 代码。|
|**仅限本机**|调试应用程序中的本机 C/C++ 代码。 忽略托管代码和 JavaScript 代码。|
|**混合(托管和本机)**|调试应用程序中的本机 C/C++ 代码和托管代码。 忽略 JavaScript 代码。 在C++项目中，此选项称为 "**托管" 和 "本机**"。|
|**脚本**|调试应用程序中的 JavaScript 代码。 忽略托管代码和本机代码。|
|**带脚本的本机**|调试应用程序中C++的本机 C/代码和 JavaScript 代码。 托管代码将被忽略。 仅适用C++于项目或后台任务。|
|**仅限 GPU (C++ AMP)**|调试在图形处理单元 (GPU) 上运行的本机 C++ 代码。 仅适用C++于项目。|

### <a name="BKMK__Optional__Disable_network_loopbacks"></a>禁用网络环回（可选）

 为了安全，以标准方式安装的 UWP 应用无法对安装它的设备进行网络调用。 默认情况下，Visual Studio 豁免使用此规则部署的应用，因此你可以在一台计算机上测试通信过程。 在发布你的应用程序之前，应在没有例外的情况下测试你的应用程序。

**若要移除网络环回例外，请执行以下操作：**

- 对于C#和 Visual Basic 应用，请取消选中 "**调试**" 属性页上的 "**启动选项**" 下的 "**允许本地网络环回**" 复选框。

- 对于C++应用，从 "**调试**" 属性页上的 "**允许本地网络环回**" 下拉列表中选择 "**否**"。

### <a name="BKMK__Optional__Reinstall_the_app_when_you_start_debugging"></a>开始调试时重新安装应用（可选）
 若要诊断C#或 Visual Basic 应用的安装问题，请选择 "**调试**" 属性页上的 "**卸载并重新安装我的程序包**"。 此选项在你开始调试时重新创建原始安装。 此选项不适用于C++项目。

### <a name="BKMK__Optional__Disable_authentication_requirement_to_start_the_remote_debugger"></a>设置远程调试的身份验证选项

默认情况下，你在选择 "**远程计算机**" 作为部署目标时，必须提供 Windows 凭据才能运行远程调试器。 可以更改身份验证要求。

**通用（未加密协议）** 身份验证模式适用于 IoT、Xbox 和 HoloLens 设备，以及创建者的更新或更高版本的 Windows 10 电脑。

**更改身份验证方法：**

- 对于C#和 Visual Basic 应用，在 "**调试**" 属性页上，选择 "**远程计算机**" 作为**目标设备**。 然后，选择 "**无**" 或 "**通用（未加密的协议）** " 作为**身份验证模式**。

- 对于C++应用，请在 "**调试**" 属性页上选择 "**要启动的调试器**" 下的 "**远程计算机**"。 然后，选择 "**无身份验证**" 或 "**通用（未加密的协议）** " 作为**身份验证类型**。

> [!CAUTION]
> 在**无**或**通用（未加密的协议）** 模式下运行远程调试器时，不会出现网络安全。 仅在受信任的网络上选择这些模式，这些模式可确保不会遭受恶意代码或恶意流量的威胁。

## <a name="BKMK_Start_the_debugging_session"></a>调试启动选项

选择 "**调试**"  >  "**开始调试**" 或按**F5**时，Visual Studio 会在附加调试器的情况下启动应用。 持续执行至抵达某个断点、手动暂停执行、发生无法处理的异常或应用程序结束为止。

### <a name="BKMK_Start_debugging__F5__but_delay_the_app_start"></a>开始调试但延迟应用启动

默认情况下，启动调试时，Visual Studio 会立即启动应用程序。 你还可以将应用程序设置为在调试模式下运行，但在调试器外部启动该应用程序。 例如，你可能需要从 Windows "**开始**" 菜单调试应用启动，或在应用中调试后台进程。 如果选择此选项，应用程序将在启动时启动。

**禁用自动应用启动：**

- 对于C#和 Visual Basic 应用，请在 "**调试**" 属性页上选择 "**不启动，但在启动时调试代码**"。

- 对于C++应用，从 "**调试**" 属性页上的 "**启动应用程序**" 下拉列表中选择 "**否**"。

有关调试后台任务的详细信息，请参阅[触发 UWP 应用的挂起、继续和后台事件](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)。

### <a name="BKMK_Start_an_installed_app_in_the_debugger"></a>调试已安装或正在运行的 UWP 应用

可以使用 "**调试安装的应用包**" 调试已在本地或远程设备上安装或运行的 UWP 应用。 此应用可能是从 Microsoft Store 安装的，也可能不是 Visual Studio 项目。 例如，应用可能有一个不使用 Visual Studio 的自定义生成系统。

可以立即启动已安装的应用程序，也可以将其设置为在以其他方法启动时在调试器中运行。 有关详细信息，请参阅[触发 UWP 应用的挂起、继续和后台事件](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)。

若要在调试器中启动已安装或正在运行的 UWP 应用，请选择 "**调试**"  > **其他调试目标** > **调试安装的应用包**。 有关更多说明，请参阅[调试已安装的应用程序包](../debugger/debug-installed-app-package.md)。

### <a name="BKMK_Attach_the_debugger_to_a_running_app_"></a>将调试器附加到正在运行的 Windows 8.x 应用

若要将调试器附加到 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 应用程序，必须使用可调式包管理器将应用程序设置为以调试模式运行。 可调试包管理器随 Visual Studio 远程工具一起安装。

1. 将 Visual Studio 远程工具安装在安装了应用的设备上。 有关详细信息，请参阅[安装远程工具](../debugger/remote-debugging.md)。

1. 在 Windows 的 "**开始**" 屏幕中，搜索并启动 "可**调试包管理器**"。

   随后显示 PowerShell 窗口，该窗口针对 AppxDebug cmdlet 进行了正确的配置。

1. 指定应用程序的 PackageFullName 标识符。

   1. 若要查看包含所有应用的 PackageFullName 的列表，请在 PowerShell 提示符下键入 `Get-AppxPackage`。

   1. 在 PowerShell 提示符下，输入 `Enable-AppxDebug <PackageFullName>`，其中 \<PackageFullName > 是应用的 PackageFullName 标识符。

1. 选择“调试” > “附加到进程”。

1. 在 "**附加到进程**" 对话框中，在 "**连接目标**" 框中指定远程设备。

   您可以输入设备名称，从 "**连接目标**" 框中的下拉列表中选择它，也可以在 "**远程连接**" 对话框中选择 "**查找**" 以查找设备。

1. 若要指定要调试的代码类型，请在 "**附加到**" 框旁选择 "**选择**"。

1. 在 "**选择代码类型**" 对话框中，选择以下任一项：
   - **自动确定要调试的代码类型**，或
   - **调试这些代码类型**，然后从列表中选择一个或多个代码类型。

1. 在 "**可用进程**" 列表中，选择要调试的应用程序进程。

1. 选择“附加”。

 Visual Studio 将调试器附加到该进程。 持续执行至抵达某个断点、手动暂停执行、发生无法处理的异常或应用程序结束为止。

::: moniker range="vs-2017"
> [!NOTE]
> JavaScript 应用使用“wwahost.exe”进程的实例运行。 如果有多个 JavaScript 应用正在运行，则需要知道要附加到应用程序的*wwahost.exe*进程的数值进程 ID （PID）。
>
> 附加到 JavaScript 应用程序的最简单方法是关闭所有其他 JavaScript 应用。 或者，你可以记下在启动应用之前，在 Windows 任务管理器中运行*wwahost.exe*进程的 pid。 当你启动应用程序时，它的*Wwahost.exe* PID 将与前面提到的程序不同。
::: moniker-end

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中调试应用](../debugger/debugging-windows-store-and-windows-universal-apps.md)