---
title: 部署 UWP 应用 |Microsoft Docs
ms.custom: seodec18
ms.date: 01/16/2018
ms.topic: conceptual
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
ms.openlocfilehash: b2fa0bd62b88602ee5a4d5091821e2c2a18f6374
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72430758"
---
# <a name="deploy-uwp-apps-from-visual-studio"></a>从 Visual Studio 部署 UWP 应用

Visual Studio 部署功能在目标设备上构建并注册使用 Visual Studio 创建的 UWP 应用。 应用的实际注册方法取决于目标设备是本地还是远程：

- 如果目标是本地 Visual Studio 计算机，Visual Studio 将从其生成文件夹注册应用。

- 如果目标是远程设备，Visual Studio 会将所需的文件复制到远程计算机并在该设备上注册应用。

从 Visual Studio 调试你的应用时，部署是自动进行的，调试方法是使用**开始调试**选项（键盘：F5）或**启动但不调试**选项 （键盘： CTRL+F5）。 你也可以手动部署应用。 手动部署在以下情况中非常有用：

- 在本地或远程计算机上进行特别测试。

- 要部署的应用将启动另一个要调试的应用。

- 部署由另一个应用或方法启动时才进行调试的应用。

## <a name="BKMK_How_to_deploy_a_Windows_Store_app"></a>如何部署 UWP 应用
 手动部署应用是一个非常简单的过程：

1. 如果你要部署到远程设备，请在应用的启动项目的属性项目页中指定设备的名称或 IP 地址。 （执行此操作的步骤在本主题靠后的位置列出)。

2. 在调试器的 Visual Studio 工具栏上，从**开始调试**按钮旁的下拉列表中选择部署目标。

     ![在本地计算机上运行](../debugger/media/vsrun_f5_local.png "VSRUN_F5_Local")

3. 在 **“生成”** 菜单上，选择 **“部署”**

## <a name="BKMK_How_to_specify_a_remote_device"></a> 如何指定远程设备

**系统必备**

在 Windows 10 远程设备上，必须启用[开发人员模式](/windows/uwp/get-started/enable-your-device-for-development)。 在运行创建者更新或更高版本的 Windows 10 设备上，在部署应用时将自动安装远程工具。 有关详细信息，请参阅[调试已安装的应用程序包](../debugger/debug-installed-app-package.md)。

> [!NOTE]
> 在 Windows 10 的预创建者更新版本中，必须在远程设备上安装 Visual Studio 远程工具，并且必须运行远程调试器。

部署使用远程调试器网络渠道将应用文件发送到远程设备。

#### <a name="to-specify-a-remote-device"></a>指定远程设备

1. 在启动项目的“调试”属性页上，指定远程部署目标的名称或 IP 地址。

2. 要打开“调试”属性页，请在解决方案资源管理器中选择项目，然后从快捷菜单中选择 **“属性”** 。

3. 然后，在属性页窗口上选择 **“调试”** 节点。

4. 对于 "**目标设备**"，选择 "**远程计算机**"。

5. 在**远程计算机** 下，单击**查找**。

6. 您可以键入远程设备的名称或 IP 地址，也可以从**远程连接**对话框选择设备。

    !["选择远程调试器连接" 对话框](../debugger/media/vsrun_selectremotedebuggerdlg.png "VSRUN_SelectRemoteDebuggerDlg")

    **远程连接**对话框中显示本地网络子网上的设备，和通过以太网电缆直接连接到 Visual Studio 计算机的任何设备。

   **在C++项目页中指定远程设备**

   ![用于&#43; &#43;远程调试的 C 项目属性](../debugger/media/vsrun_cpp_projprop_remote.png "VSRUN_CPP_ProjProp_Remote")

7. 从 **要启动的调试器** 列表中选择 **远程调试器** 。

8. 在 **“计算机名称”** 框中输入远程设备的网络名称。 或者，你可以选择框中的下拉箭头，从“选择远程调试器连接”对话框中选择该设备。

   **在 Visual C# 和 Visual Basic 项目页中指定远程设备**

   ![用于远程调试的托管项目属性](../debugger/media/vsrun_managed_projprop_remote.png "VSRUN_Managed_ProjProp_Remote")

9. 对于**目标设备**，选择**远程计算机**。

10. 在 **“远程计算机”** 框中输入远程设备的网络名称，或单击 **“查找”** ，从 **“选择远程调试器连接”** 对话框中选择该设备。

## <a name="BKMK_Deployment_options"></a> 部署选项

你可以在启动项目的“调试”属性页上设置以下部署选项。

**允许网络环回**

出于安全原因，以标准方式安装的 UWP 或 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 应用程序不可以对其所在的设备进行网络调用。 默认情况下，Visual Studio 部署功能会针对部署的应用为此规则创建一个例外。 通过此例外，你可以在一台计算机上测试通信过程。 向 [!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)] 提交应用之前，应该在不使用该例外的情况下测试你的应用。

若要从应用中移除网络环回例外，请执行以下操作：

- 在 " C#调试 Visual Basic" 属性页上，清除 "**允许网络环回**" 复选框。

- 在 " C++调试" 属性页上，将 "**允许网络环回**" 值设置为 "**否**"。

**不启动，但在启动（C#和 Visual Basic）/启动应用程序（）时调试我C++的代码（）**

将部署配置为在应用程序启动时，自动启动调试会话：

- 在 " C#调试 Visual Basic" 属性页上，选中 "不**启动，但在启动时调试代码**" 复选框。

- 在 " C++调试" 属性页上，将 "**启动应用程序**" 值设置为 **"是"** 。

## <a name="see-also"></a>请参阅

- [高级远程部署选项](/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps#advanced-remote-deployment-options)
- [调试安装的应用包](../debugger/debug-installed-app-package.md)
- [从 Visual Studio 运行应用](/visualstudio/debugger/debugging-windows-store-and-windows-universal-apps)
