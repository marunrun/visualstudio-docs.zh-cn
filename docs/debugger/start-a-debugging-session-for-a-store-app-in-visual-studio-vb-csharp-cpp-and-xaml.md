---
title: 启动 UWP 应用的调试会话 | Microsoft Docs
ms.custom: seodec18
ms.date: 11/20/2018
ms.topic: how-to
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
ms.openlocfilehash: c4e025603fef11e278aee21b3c44f8d35d7cd34b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536547"
---
# <a name="start-a-debugging-session-for-a-uwp-app"></a>启动 UWP 应用的调试会话

本文介绍如何启动通用 Windows 平台 (UWP) 应用的 Visual Studio 调试会话。 UWP 应用可以采用 XAML 和 C++、XAML 和 C#/Visual Basic 编写。 若要开始调试 UWP 应用，请配置调试会话并选择启动应用的方式。

::: moniker range=">=vs-2019"
> [!NOTE]
> 从 Visual Studio 2019 开始，不再支持针对 HTML 和 JavaScript 的 UWP 应用。
::: moniker-end
::: moniker range="vs-2017"
在 Visual Studio 2017 中，本文中所示的大多数命令和选项还适用于针对 HTML 和 JavaScript 的 UWP 应用。 托管应用与 C++ 应用之间的命令不同，而 JavaScript 应用通常与 C++ UWP 应用的命令相同。
::: moniker-end

## <a name="start-debugging-from-the-visual-studio-toolbar"></a><a name="BKMK_The_easy_way_to_start_debugging"></a>从 Visual Studio 工具栏启动调试

配置和启动调试的最简单方法是在标准 Visual Studio 工具栏中进行。

![从工具栏调试](../debugger/media/vsrun_select_target_device.png)

1. 从“标准”工具栏上的“配置”下拉菜单中，选择“调试”。

1. 从“平台”下拉菜单中，选择要为其进行生成的目标平台。

1. 从绿色箭头旁的下拉菜单中，选择调试目标。 可以选择本地计算机、直接连接的设备、本地 Visual Studio 模拟器、远程设备或仿真器。

1. 若要启动调试，请选择工具栏上的绿色“启动”箭头，或选择“调试” > “启动调试”，或按 F5。

   Visual Studio 生成并启动附有调试器的应用程序。

持续调试至抵达某个断点、手动暂停执行、发生无法处理的异常或应用结束为止。

### <a name="deployment-target-options"></a><a name="BKMK_Choose_the_deployment_target"></a> 部署目标选项

可以在 Visual Studio 工具栏或项目的调试属性页中设置调试目标。 选择下列选项之一：

|“属性”|描述|
|-|-|
|**本地计算机**|在本地计算机上的当前会话中调试应用程序。|
|**模拟器**|在 UWP 应用的 Visual Studio 模拟器中调试应用。 模拟器是一个桌面窗口，可模拟本地计算机上可能未提供的设备功能，如触摸手势和设备旋转。 仅当应用的“目标平台最低版本”小于或等于本地计算机上的操作系统时，模拟器选项才可用。 有关详细信息，请参阅[在模拟器中运行 UWP 应用](../debugger/run-windows-store-apps-in-the-simulator.md)。|
|**远程计算机**|在通过网络或以太网电缆连接到本地计算机的设备上调试应用。 Visual Studio 远程工具必须已在远程设备上安装并运行。 有关详细信息，请参阅[在远程计算机上运行 UWP 应用](../debugger/run-windows-store-apps-on-a-remote-machine.md)。|
|**设备**|在 USB 连接的设备上调试应用。 设备必须已由开发人员解锁，并使屏幕处于解锁状态。|
|Mobile 仿真器|启动在仿真器名称中指定的仿真器，部署应用，并启动调试。 仿真器仅在支持 Hyper-V 的计算机上可用。|

## <a name="configure-debugging-in-the-project-property-page"></a><a name="BKMK_Open_the_debugging_property_page_for_the_project"></a> 在项目属性页中配置调试

若要配置其他调试选项，请使用项目的调试属性页。

若要打开调试属性，请执行以下操作：

1. 在“解决方案资源管理器”中，选择项目，然后选择“属性”图标，或右键单击项目并选择“属性”  。

1. 在“属性”窗格的左侧：

   - 对于 C# 和 Visual Basic 应用，选择“调试”。

     ![C# 和 Visual Basic 项目调试属性页](../debugger/media/dbg_csvb_debugpropertypage.png)

   - 对于 C++ 应用，选择“配置属性” > “调试”。

     ![C++ UWP 应用调试属性页](../debugger/media/dbg_cpp_debugpropertypage.png)

### <a name="choose-the-debugger-to-use"></a><a name="BKMK_Choose_the_debugger_to_use"></a> 选择要使用的调试器

对于 C# 和 Visual Basic 应用，默认情况下，Visual Studio 会调试托管代码。 可以选择调试其他或附加代码类型。 还可以为属于项目的任何后台任务设置“调试器类型”值。

在 C++ 应用中，默认情况下，Visual Studio 会调试本机代码。 可以选择调试特定类型的代码而不调试本机代码，或也调试本机代码。

若要指定要调试的代码类型，请执行以下操作：

- 对于 C# 和 Visual Basic 应用，在“调试”属性页上的“调试器类型”下，从“应用程序类型”和“后台进程类型”下拉菜单中选择以下调试器之一   。

- 对于 C++ 应用，从“调试”属性页上的“调试器类型”下拉菜单中选择以下调试器之一 。

|“属性”|描述|
|-|-|
|**仅限托管**|调试应用程序中的托管代码。 忽略 JavaScript 代码和本机 C/C++ 代码。|
|**仅限本机**|调试应用程序中的本机 C/C++ 代码。 忽略托管代码和 JavaScript 代码。|
|**混合(托管和本机)**|调试应用程序中的本机 C/C++ 代码和托管代码。 忽略 JavaScript 代码。 在 C++ 项目中，此选项称为“托管和本机”。|
|**脚本**|调试应用程序中的 JavaScript 代码。 忽略托管代码和本机代码。|
|**带脚本的本机**|调试应用中的本机 C/C++ 代码和 JavaScript 代码。 忽略托管代码。 仅适用于 C++ 项目或后台任务。|
|**仅限 GPU (C++ AMP)**|调试在图形处理单元 (GPU) 上运行的本机 C++ 代码。 仅适用于 C++ 项目。|

### <a name="disable-network-loopbacks-optional"></a><a name="BKMK__Optional__Disable_network_loopbacks"></a> 禁用网络环回（可选）

 为安全起见，以标准方式安装的 UWP 应用无法对装有它的设备进行网络调用。 默认情况下，Visual Studio 会从此规则中排除已部署的应用，因此可以在单台计算机上测试通信过程。 发布应用之前，应该在没有例外的情况下测试你的应用。

**若要移除网络环回例外，请执行以下操作：**

- 对于 C# 和 Visual Basic 应用，在“调试”属性页上的“启动选项”下取消选中“允许网络环回”  复选框。

- 对于 C++ 应用，从“调试”属性页上的“允许本地网络环回”下拉菜单中选择“否”  。

### <a name="reinstall-the-app-when-you-start-debugging-optional"></a><a name="BKMK__Optional__Reinstall_the_app_when_you_start_debugging"></a> 在启动调试时重新安装应用（可选）
 若要诊断 C# 或 Visual Basic 应用的安装问题，请在“调试”属性页上选择“卸载并重新安装我的包” 。 此选项在启动调试时重新创建原始安装。 此选项不适用于 C++ 项目。

### <a name="set-authentication-options-for-remote-debugging"></a><a name="BKMK__Optional__Disable_authentication_requirement_to_start_the_remote_debugger"></a> 为远程调试设置身份验证选项

默认情况下，在选择“远程计算机”作为部署目标时，必须提供 Windows 凭据才能运行远程调试器。 可以更改身份验证要求。

“通用(未加密协议)”通用身份验证模式适用于 IoT、Xbox 和 HoloLens 设备，以及创建者的更新或更高版本的 Windows 10 电脑。

若要更改身份验证方法，请执行以下操作：

- 对于 C# 和 Visual Basic 应用，在“调试”属性页上，选择“远程计算机”作为“目标设备”  。 然后，对“身份验证模式”选择“无”或“通用(未加密协议)”  。

- 对于 C++ 应用，在“调试”属性页上的“要启动的调试器”下选择“远程计算机”  。 然后，对“身份验证类型”选择“无身份验证”或“通用(未加密协议)”  。

> [!CAUTION]
> 在“无”或“通用(未加密协议)”模式下运行远程调试器时，没有网络安全。 仅在确定不会遇到恶意代码或恶意通信的受信任网络上，才选择这些模式。

## <a name="debugging-start-options"></a><a name="BKMK_Start_the_debugging_session"></a> 调试启动选项

选择“调试” > “启动调试”或按 F5 时，Visual Studio 启动附带调试器的应用。 持续执行至抵达某个断点、手动暂停执行、发生无法处理的异常或应用程序结束为止。

### <a name="start-debugging-but-delay-app-start"></a><a name="BKMK_Start_debugging__F5__but_delay_the_app_start"></a> 启动调试，但延迟启动应用

默认情况下，启动调试后，Visual Studio 将立即启动应用。 也可以将应用设置为在调试模式中运行，但是在调试器之外启动应用。 例如，可能要从 Windows“开始”菜单中调试应用启动，或在应用中调试后台进程。 如果选择此选项，则应用在启动时会在调试器中启动。

若要禁用自动应用启动，请执行以下操作：

- 对于 C# 和 Visual Basic 应用，在“调试”属性页上的“启动选项”下选择“不启动，但在启动时调试代码”  。

- 对于 C++ 应用，从“调试”属性页上的“启动应用程序”下拉菜单中选择“否”  。

有关调试后台任务的详细信息，请参阅[为 UWP 应用触发挂起、继续和后台事件](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)。

### <a name="debug-an-installed-or-running-uwp-app"></a><a name="BKMK_Start_an_installed_app_in_the_debugger"></a> 调试已安装或正在运行的 UWP 应用

可以使用“调试安装的应用程序包”调试已在本地或远程设备上安装或运行的 UWP 应用。 应用可能是从 Microsoft Store 安装，也可能不是 Visual Studio 项目。 例如，应用可能具有不使用 Visual Studio 的自定义生成系统。

可以立即启动已安装的应用，也可以将它设置为在以其他方法启动时在调试器中运行。 有关详细信息，请参阅[为 UWP 应用触发挂起、继续和后台事件](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)。

若要在调试器中启动已安装或正在运行的 UWP 应用，请选择“调试” > “其他调试目标” > “调试安装的应用程序包”。 有关更多说明，请参阅[调试安装的应用包](../debugger/debug-installed-app-package.md)。

### <a name="attach-the-debugger-to-a-running-windows-8x-app"></a><a name="BKMK_Attach_the_debugger_to_a_running_app_"></a> 将调试器附加到正在运行的 Windows 8.x 应用

若要将调试器附加到 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 应用程序，必须使用可调式包管理器将应用程序设置为以调试模式运行。 可调式包管理器与 Visual Studio 远程工具一并安装。

1. 在装有应用的设备上安装 Visual Studio 远程工具。 有关详细信息，请参阅[安装远程工具](../debugger/remote-debugging.md)。

1. 在 Windows“启动”屏幕上，搜索并启动“可调试包管理器”。

   随后显示 PowerShell 窗口，该窗口针对 AppxDebug cmdlet 进行了正确的配置。

1. 指定应用的 PackageFullName 标识符。

   1. 若要查看包含所有应用的 PackageFullName 的的列表，请在 PowerShell 提示符下键入 `Get-AppxPackage`。

   1. 在 PowerShell 提示符下，输入 `Enable-AppxDebug <PackageFullName>`，其中 \<PackageFullName> 是应用的 PackageFullName 标识符。

1. 选择“调试” > “附加到进程” 。

1. 在“附加到进程”对话框中，在“连接目标”框中指定远程设备。

   可以在“远程连接”对话框中输入设备名称，从“连接目标”框中的下拉菜单中选择它，或选择“查找”以查找设备。

1. 若要指定要调试的代码类型，请在“附加到”框旁，选择“选择”。

1. 在“选择代码类型”对话框中，选择以下任一项：
   - “自动确定要调试的代码类型”，或者
   - “调试以下代码类型”，然后从列表中选择一个或多个类型。

1. 在“可用进程”列表中，选择要调试的应用进程。

1. 选择“附加”。

 Visual Studio 将调试器附加到该进程。 持续执行至抵达某个断点、手动暂停执行、发生无法处理的异常或应用程序结束为止。

::: moniker range="vs-2017"
> [!NOTE]
> JavaScript 应用使用“wwahost.exe”进程的实例运行。 如果有多个 JavaScript 应用正在运行，则需要知道要附加到应用的 wwahost.exe 进程的数字进程 ID (PID)。
>
> 附加到 JavaScript 应用的最简单方法是关闭所有其他 JavaScript 应用。 或者，可以在启动应用之前，在 Windows 任务管理器中记下正在运行的 wwahost.exe 进程的 PID。 启动你的应用时，其 wwahost.exe PID 会与前面记下的 PID 不同。
::: moniker-end

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中调试应用](../debugger/debugging-windows-store-and-windows-universal-apps.md)