---
title: 调试远程计算机上的 UWP 应用 |Microsoft Docs
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62902851"
---
# <a name="debug-uwp-apps-on-remote-machines-from-visual-studio"></a>调试从 Visual Studio 的远程计算机上的 UWP 应用

Visual Studio 可用于运行、 调试、 分析和测试另一台计算机或设备上的通用 Windows 平台 (UWP) 应用。 在 Visual Studio 计算机不支持特定于 UWP 的功能，例如触摸、 地理位置或物理方向时，在远程计算机上运行 UWP 应用将非常有用。

## <a name="BKMK_Prerequisites"></a> 先决条件

若要调试从 Visual Studio 在远程设备上的 UWP 应用：

- Visual Studio 项目必须配置用于远程调试。
- 远程计算机和 Visual Studio 计算机必须通过网络连接或通过 USB 或以太网电缆直接连接。 不支持通过 Internet 进行调试。
- 您必须[开发人员模式下打开](/windows/uwp/get-started/enable-your-device-for-development)Visual Studio 计算机和远程计算机上。
- 远程计算机必须运行远程工具用于 Visual Studio。
  - 某些 Windows 10 版本启动并自动运行的远程工具。 否则为[安装和运行 Visual Studio 远程工具](#BKMK_download)。
  - Windows 10 移动设备不需要或支持远程工具。

## <a name="BKMK_ConnectVS"></a> 配置 Visual Studio 项目以便进行远程调试
<a name="BKMK_DirectConnect"></a> 使用项目**属性**来指定要连接到的远程设备。 设置不同，具体取决于编程语言。

> [!CAUTION]
> 默认情况下，属性页用于设置**通用 （未加密的协议）** 作为**身份验证类型**为 Windows 10 的远程连接。 可能需要设置**无身份验证**连接到远程调试器。 **通用 （未加密的协议）** 并**无身份验证**协议有任何网络安全，因此开发和远程计算机之间传递的数据是易受攻击。 选择这些身份验证类型仅用于受信任网络，确保不可遭受恶意通信的情况。
>
>如果愿意**Windows 身份验证**有关**身份验证类型**，将需要登录到远程计算机调试时。 此外必须在运行远程调试器**Windows 身份验证**模式下，作为 Visual Studio 计算机上的同一用户帐户。

### <a name="BKMK_Choosing_the_remote_device_for_C__and_Visual_Basic_projects"></a> 配置C#或 Visual Basic 项目进行远程调试

1. 选择C#或 Visual Studio 中的 Visual Basic 项目**解决方案资源管理器**，然后选择**属性**图标，按**Alt** + **输入**，或右键单击，然后选择**属性**。

1. 选择“调试”选项卡。

1. 下**目标设备**，选择**远程计算机**远程计算机，或**设备**直接连接的 Windows 10 移动设备。

1. 对于远程计算机，请输入网络名称或 IP 地址**远程计算机**字段，也可以选择**查找**搜索中的设备[远程连接对话框的](#remote-connections)。

    ![管理项目属性以便进行远程调试](../debugger/media/vsrun_managed_projprop_remote.png "托管调试项目属性")

### <a name="BKMK_Choosing_the_remote_device_for_JavaScript_and_C___projects"></a> 配置C++项目以便进行远程调试

1. 选择C++在 Visual Studio 中的项目**解决方案资源管理器**，然后选择**属性**图标，按**Alt**+**Enter**，或右键单击，然后选择**属性**。

1. 选择**调试**选项卡。

3. 下**要启动的调试器**，选择**远程计算机**远程计算机，或**设备**直接连接的 Windows 10 移动设备。

1. 对于远程计算机中，输入或选择网络名称或 IP 地址**计算机名称**字段中或向下和选择的下拉**定位**搜索中的设备[远程连接对话框](#remote-connections).

    ![C++项目属性以便进行远程调试](../debugger/media/vsrun_cpp_projprop_remote.png " C++调试项目属性")

### <a name="remote-connections"></a> 使用远程连接对话框

在中**远程连接**对话框中，可以搜索特定的远程计算机名称或 IP 地址，也可以自动检测连接通过选择舍入箭头刷新图标。 在对话框中搜索仅当前正在运行远程调试器的设备上的本地子网。 可以在检测到不是所有设备**远程连接**对话框。

 ![远程连接对话框](../debugger/media/vsrun_selectremotedebuggerdlg.png "远程连接对话框")

>[!TIP]
>如果不能按名称连接到远程设备，请尝试使用其 IP 地址。 若要确定 IP 地址，在远程设备上，输入**ipconfig**命令窗口中。 IP 地址显示为**IPv4 地址**。

## <a name="BKMK_download"></a> 为 Visual Studio 下载和安装远程工具

对于 Visual Studio 中调试远程计算机上的应用，在远程计算机必须运行远程工具用于 Visual Studio。

- Windows 10 移动设备不需要或支持远程工具。
- 运行创建者的 Windows 10 电脑的更新 (1703 版本) 以及更高版本，Windows 10 Xbox、 IoT 和 HoloLens 设备安装远程工具自动部署应用时。
- Pre-创建者的更新 Windows 10 电脑，必须手动下载、 安装和开始调试之前，在远程计算机上运行远程工具。

**若要下载并安装远程工具：**

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

### <a name="BKMK_setup"></a> 配置远程工具

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

## <a name="BKMK_RunRemoteDebug"></a> 远程调试 UWP 应用

远程调试的工作方式相同的本地调试。

1. 在之前的创建者的更新版本的 Windows 10，请确保远程调试监视器 (*msvsmon.exe*) 在远程设备上运行。

1. 在 Visual Studio 计算机上，请确保正确的调试目标 (**远程计算机**或**设备**) 工具栏上的绿色箭头旁边会显示。

1. 开始调试通过选择**调试** > **开始调试**，按**F5**，或选择工具栏上的绿色箭头。

   项目重新编译，然后部署和启动远程设备上。 调试器在断点处挂起执行，并可以单步执行、 逐过程和跳出代码。

1. 如有必要，选择**调试** > **停止调试**或按**Shift**+**F5**以停止调试并关闭远程应用程序。

## <a name="see-also"></a>请参阅
- [高级远程部署选项](/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps#advanced-remote-deployment-options)
- [使用 Visual Studio 测试 UWP 应用](/visualstudio/test/create-and-run-unit-tests-for-a-store-app-in-visual-studio/)
- [在 Visual Studio 中调试 UWP 应用](debugging-windows-store-and-windows-universal-apps.md)
