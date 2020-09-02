---
title: 部署 Windows 应用商店应用
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: ef3a0f36-bfc9-4ca0-aa61-18261f619bff
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 73b4350a2e7f277a11f4d6650d8089df0f87fe4d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68177487"
---
# <a name="deploy-windows-store-apps-from-visual-studio"></a>从 Visual Studio 部署 Windows 应用商店应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

仅适用于 Windows (）。将 windows_only_content.png "windows_only_content" ) 

 Visual Studio 部署功能可在目标设备上生成和注册随 Visual Studio 创建的 Windows 应用商店应用。 应用的实际注册方法取决于目标设备是本地还是远程：

- 如果目标是本地 Visual Studio 计算机，Visual Studio 将从其生成文件夹注册应用。

- 如果目标是远程设备，Visual Studio 会将所需的文件复制到远程计算机并在该设备上注册应用。

  从 Visual Studio 调试应用时，部署是自动的，调试方法是使用“启动调试”选项（键盘：F5）或“在不调试的情况下启动”选项（键盘：CTRL + F5）。 你也可以手动部署应用。 手动部署在以下情况中非常有用：

- 在本地或远程计算机上进行特别测试。

- 要部署的应用将启动另一个要调试的应用。

- 部署由另一个应用或方法启动时才进行调试的应用。

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> 在本主题中
 在本主题中，你将了解：

 [如何部署 Windows 应用商店应用程序](#BKMK_How_to_deploy_a_Windows_Store_app)

 [如何指定远程设备](#BKMK_How_to_specify_a_remote_device)

 [部署选项](#BKMK_Deployment_options)

## <a name="how-to-deploy-a-windows-store-app"></a><a name="BKMK_How_to_deploy_a_Windows_Store_app"></a> 如何部署 Windows 应用商店应用
 手动部署应用是一个非常简单的过程：

1. 如果你要部署到远程设备，请在应用的启动项目的属性项目页中指定设备的名称或 IP 地址。 （执行此操作的步骤在本主题靠后的位置列出)。

2. 在调试器的 Visual Studio 工具栏上，从**开始调试**按钮旁的下拉列表中选择部署目标。

     ![在本地计算机上运行](../debugger/media/vsrun-f5-local.png "VSRUN_F5_Local")

3. 在 **“生成”** 菜单上，选择 **“部署”**

## <a name="how-to-specify-a-remote-device"></a><a name="BKMK_How_to_specify_a_remote_device"></a> 如何指定远程设备
 **系统必备**

 将应用部署到远程设备：

- 必须在远程设备上安装开发人员许可证。

- 远程设备上必须已安装 Visual Studio 远程工具并且远程调试监视器必须正在运行。

     部署使用远程调试器网络渠道将应用文件发送到远程设备。

#### <a name="to-specify-a-remote-device"></a>指定远程设备

1. 在启动项目的“调试”属性页上，指定远程部署目标的名称或 IP 地址。

2. 要打开“调试”属性页，请在解决方案资源管理器中选择项目，然后从快捷菜单中选择 **“属性”** 。

3. 然后，在属性页窗口上选择 **“调试”** 节点。

4. 你可以键入远程设备的名称或 IP 地址，也可以从 **“选择远程调试器连接”** 对话框选择该设备。

    ![“选择远程调试器连接”对话框](../debugger/media/vsrun-selectremotedebuggerdlg.png "VSRUN_SelectRemoteDebuggerDlg")

    **“选择远程调试器连接”** 对话框显示本地子网上的设备以及通过以太网电缆直接连接到 Visual Studio 计算机的任何设备。

   **在 JavaScript 或 Visual C++ 项目页中指定远程设备**

   ![用于远程调试的 C++ 项目属性](../debugger/media/vsrun-cpp-projprop-remote.png "VSRUN_CPP_ProjProp_Remote")

5. 从 **要启动的调试器** 列表中选择 **远程调试器** 。

6. 在 **“计算机名称”** 框中输入远程设备的网络名称。 或者，你可以选择框中的下拉箭头，从“选择远程调试器连接”对话框中选择该设备。

   **在 Visual C# 和 Visual Basic 项目页中指定远程设备**

   ![用于远程调试的托管项目属性](../debugger/media/vsrun-managed-projprop-remote.png "VSRUN_Managed_ProjProp_Remote")

7. 对于**目标设备**，选择**远程计算机**。

8. 在 **“远程计算机”** 框中输入远程设备的网络名称，或单击 **“查找”** ，从 **“选择远程调试器连接”** 对话框中选择该设备。

## <a name="deployment-options"></a><a name="BKMK_Deployment_options"></a> 部署选项
 你可以在启动项目的“调试”属性页上设置以下部署选项。

 **允许网络环回** 出于安全原因， [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] 不允许以标准方式安装的应用程序对安装它的设备进行网络调用。 默认情况下，Visual Studio 部署功能会针对部署的应用为此规则创建一个例外。 通过此例外，你可以在一台计算机上测试通信过程。 向 [!INCLUDE[win8_appstore_long](../includes/win8-appstore-long-md.md)] 提交应用之前，应该在不使用该例外的情况下测试你的应用。

 若要从应用中移除网络环回例外，请执行以下操作：

- 在 C# 和 VB 调试属性页上，清除 **“允许网络环回”** 复选框。

- 在 JavaScript 和调试属性页上，将 **“允许网络环回”** 值设置为 **“否”**。

  不**启动，但在启动时调试代码 (c # 和 VB) /启动应用程序 (JavaScript 和 c + +) **配置部署以在应用启动时自动启动调试会话：

- 在 C# 和 VB 调试属性页上，选中 **“不启动，但在启动时调试代码”** 复选框。

- 在 JavaScript 和调试属性页上，将 **“启动应用程序”** 值设置为 **“是”**。

## <a name="see-also"></a>另请参阅
 [从 Visual Studio 运行应用](../debugger/run-store-apps-from-visual-studio.md)
