---
title: 调试远程计算机上的 UWP 应用 | Microsoft Docs
ms.date: 10/05/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 0f6814d6-cd0d-49f3-b501-dea8c094b8ef
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 50d307cd65bfdf534b6ca3586e69bbc27be25e36
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62902851"
---
# <a name="debug-uwp-apps-on-remote-machines-from-visual-studio"></a>在 Visual Studio 中调试远程计算机上的 UWP 应用

可使用 Visual Studio 在其他计算机或设备上运行、调试、分析和测试通用 Windows 平台 (UWP) 应用。 当 Visual Studio 计算机不支持触摸、地理位置或物理方向等 UWP 特定功能时，在远程计算机上运行 UWP 应用特别有用。

## <a name="prerequisites"></a><a name="BKMK_Prerequisites"></a> 先决条件

要在 Visual Studio 中调试远程设备上的 UWP 应用，请执行以下操作：

- 必须配置 Visual Studio 项目进行远程调试。
- 远程计算机与 Visual Studio 计算机必须通过网络连接或直接通过 USB 或以太网电缆连接。 不支持通过 Internet 进行调试。
- 必须在 Visual Studio 计算机和远程计算机上同时[启用开发者模式](/windows/uwp/get-started/enable-your-device-for-development)。
- 远程计算机必须正在运行 Visual Studio 远程工具。
  - 某些 Windows 10 版本会自动启动并运行远程工具。 否则，请[安装并运行 Visual Studio 远程工具](#BKMK_download)。
  - Windows Mobile 10 设备不需要或不支持远程工具。

## <a name="configure-a-visual-studio-project-for-remote-debugging"></a><a name="BKMK_ConnectVS"></a> 配置 Visual Studio 项目以便进行远程调试
<a name="BKMK_DirectConnect"></a> 使用项目“属性”指定要连接到的远程设备。 这些设置因编程语言而有所不同。

> [!CAUTION]
> 对于 Windows 10 远程连接，属性页面会默认将“身份验证类型”设置为“通用(未加密协议)” 。 可能需要设置“无身份验证”才能连接到远程调试器。 “通用(未加密协议)”和“无身份验证”协议没有网络安全保障，因此在开发计算机和远程计算机之间传递的数据很容易受到攻击 。 仅在确定不会遇到恶意攻击或恶意通信的受信任网络上，才选择这些身份验证类型。
>
>如果将“身份验证类型”设置为“Windows 身份验证”，则在调试时需要登录到远程计算机 。 远程调试器还必须在“Windows 身份验证”模式下运行，并且使用与 Visual Studio 计算机相同的用户帐户。

### <a name="configure-a-c-or-visual-basic-project-for-remote-debugging"></a><a name="BKMK_Choosing_the_remote_device_for_C__and_Visual_Basic_projects"></a> 配置 C# 或 Visual Basic 项目以便进行远程调试

1. 在 Visual Studio“解决方案资源管理器”中选择 C# 或 Visual Basic 项目，然后选择“属性”图标，按 Alt+Enter，或右键单击并选择“属性”    。

1. 选择“调试”选项卡。

1. 在“目标设备”下，针对远程计算机选择“远程计算机”，针对直接连接的 Windows Mobile 10 设备选择“设备”  。

1. 对于远程计算机，请在“远程计算机”字段中输入网络名称或 IP 地址，或在[“远程连接”对话框](#remote-connections)中选择“查找”以搜索设备 。

    ![用于远程调试的托管项目属性](../debugger/media/vsrun_managed_projprop_remote.png "托管的调试项目属性")

### <a name="configure-a-c-project-for-remote-debugging"></a><a name="BKMK_Choosing_the_remote_device_for_JavaScript_and_C___projects"></a> 配置 C++ 项目以便进行远程调试

1. 在 Visual Studio“解决方案资源管理器”中选择 C++ 项目，然后选择“属性”图标，按 Alt+Enter，或右键单击并选择“属性”    。

1. 选择“调试”选项卡。

3. 在“要启动的调试器”下，针对远程计算机选择“远程计算机”，针对直接连接的 Windows Mobile 10 设备选择“设备”  。

1. 对于远程计算机，请在“计算机名称”字段中输入或选择网络名称或 IP 地址，或在[“远程连接”对话框](#remote-connections)中下拉并选择“查找”以搜索设备 。

    ![用于远程调试的 C++ 项目属性](../debugger/media/vsrun_cpp_projprop_remote.png "C++ 调试项目属性")

### <a name="use-the-remote-connections-dialog-box"></a><a name="remote-connections"></a> 使用“远程连接”对话框

在“远程连接”对话框中，可以搜索特定的远程计算机名称或 IP 地址，也可以通过选择圆角箭头刷新图标来自动检测连接。 该对话框仅搜索本地子网上当前正在运行远程调试器的设备。 并非所有设备都可在“远程连接”对话框中检测到。

 ![“远程连接”对话框](../debugger/media/vsrun_selectremotedebuggerdlg.png "“远程连接”对话框")

>[!TIP]
>如果无法按名称连接到远程设备，请尝试使用其 IP 地址。 要确定 IP 地址，请在远程设备上的命令窗口中输入 ipconfig。 IP 地址显示为“IPv4 地址”。

## <a name="download-and-install-the-remote-tools-for-visual-studio"></a><a name="BKMK_download"></a> 为 Visual Studio 下载和安装远程工具

为了使 Visual Studio 能够调试某远程计算机上的应用，该远程计算机必须运行 Visual Studio 远程工具。

- Windows Mobile 10 设备不需要或不支持远程工具。
- 部署应用时，运行创意者更新（版本 1703）及更高版本的 Windows 10 PC、Windows 10 Xbox、IoT 和 HoloLens 设备会自动安装远程工具。
- 在预创意者更新 Windows 10 PC 上，必须先在远程计算机上手动下载、安装并运行远程工具，然后才能开始调试。

**要下载和安装远程工具，请执行以下操作**：

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

### <a name="configure-the-remote-tools"></a><a name="BKMK_setup"></a> 配置远程工具

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

## <a name="debug-uwp-apps-remotely"></a><a name="BKMK_RunRemoteDebug"></a> 远程调试 UWP 应用

远程调试与本地调试方式相同。

1. 在预创意者更新版 Windows 10 上，确保远程设备正在运行远程调试监视器 (msvsmon.exe)。

1. 在 Visual Studio 计算机上，确保工具栏上的绿色箭头旁边显示了正确的调试目标（“远程计算机”或“设备”） 。

1. 通过选择“调试” > “开始调试”、按 F5 或选择工具栏上的绿色箭头来启动调试  。

   该项目将重新编译，然后在远程设备上部署并启动。 调试器在断点暂停执行，可让你单步调试、单步跳过和单步跳出代码。

1. 如有必要，请选择“调试” > “停止调试”或按 Shift+F5 以停止调试并关闭远程应用   。

## <a name="see-also"></a>请参阅
- [高级远程部署选项](/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps#advanced-remote-deployment-options)
- [使用 Visual Studio 测试 UWP 应用](/visualstudio/test/create-and-run-unit-tests-for-a-store-app-in-visual-studio/)
- [在 Visual Studio 中调试 UWP 应用](debugging-windows-store-and-windows-universal-apps.md)
