---
title: 远程调试C++项目 |Microsoft Docs
ms.custom: remotedebugging
ms.date: 08/14/2018
ms.topic: conceptual
dev_langs:
- C++
- FSharp
- CSharp
- JScript
- VB
helpviewer_keywords:
- remote debugging, setup
ms.assetid: 8b8eca0d-122f-4eda-848a-cf0945f207d0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 0173ed557afa47129e0cc92d9ef9b2d94a7b198f
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72730327"
---
# <a name="remote-debugging-a-c-project-in-visual-studio"></a>在 Visual Studio C++中远程调试项目
若要在另一台计算机上调试 Visual Studio 应用程序，请在要部署应用程序的计算机上安装并运行远程工具，将项目配置为从 Visual Studio 连接到远程计算机，然后部署并运行应用。

![远程调试器组件](../debugger/media/remote-debugger-client-apps.png "Remote_debugger_components")

有关远程调试通用 Windows 应用（UWP）的信息，请参阅[调试已安装的应用程序包](debug-installed-app-package.md)。

## <a name="requirements"></a>要求

Windows 7 和更高版本（非电话）和 windows Server 版本（从 Windows Server 2008 Service Pack 2 开始）支持远程调试器。 有关要求的完整列表，请参阅[要求](../debugger/remote-debugging.md#requirements_msvsmon)。

> [!NOTE]
> 不支持在通过代理连接的两台计算机之间进行调试。 不建议在高延迟或低带宽连接（如拨号 Internet）或跨国家/地区跨 Internet 进行调试，它们可能会失败，也可能会变得很慢。

## <a name="download-and-install-the-remote-tools"></a>下载和安装远程工具

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

> [!TIP]
> 在某些情况下，从文件共享运行远程调试器是最有效的方法。 有关详细信息，请参阅[从文件共享运行远程调试器](../debugger/remote-debugging.md#fileshare_msvsmon)。

## <a name="BKMK_setup"></a>设置远程调试器

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 如果需要添加其他用户的权限、更改身份验证模式或远程调试器的端口号，请参阅[配置远程调试器](../debugger/remote-debugging.md#configure_msvsmon)。

## <a name="remote_cplusplus"></a>远程调试C++项目
 在下面的过程中，项目的名称和路径为 C:\remotetemp\MyMfc，远程计算机的名称为**MJO**。

1. 创建名为 mymfc 的 MFC 应用程序。

2. 在应用程序中容易到达的地方设置断点，例如，在 MainFrm.cpp 中（位于 `CMainFrame::OnCreate` 的开头）。

3. 在解决方案资源管理器中，右键单击项目，然后选择 "**属性**"。 打开“调试”选项卡。

4. 将“要启动的调试器”更改为“远程 Windows 调试器”。

    ![RemoteDebuggingCPlus](../debugger/media/remotedebuggingcplus.png "RemoteDebuggingCPlus")

5. 对属性进行以下更改：

   |设置|“值”|
   |-|-|
   |远程命令|C:\remotetemp\mymfc.exe|
   |工作目录|C:\remotetemp|
   |远程服务器名称|MJO：*portnumber*|
   |连接|带 Windows 身份验证的远程访问|
   |调试器类型|仅限本机|
   |部署目录|C:\remotetemp。|
   |其他要部署的文件|C:\data\mymfcdata.txt。|

    如果部署其他文件（可选），则该文件夹必须在两台计算机上都存在。

6. 在解决方案资源管理器中，右键单击该解决方案，然后选择 " **Configuration Manager**"。

7. 对于“调试”配置，请选中“部署”复选框。

    ![RemoteDebugCplusDeploy](../debugger/media/remotedebugcplusdeploy.png "RemoteDebugCplusDeploy")

8. 开始调试（单击“调试”>“启动调试”，或按 F5）。

9. 可执行文件会自动部署到远程计算机。

10. 如果系统提示，请输入网络凭据以连接到远程计算机。

     所需的凭据特定于你的网络安全配置。 例如，在域计算机上，您可以选择一个安全证书或输入您的域名和密码。 在非域计算机上，可以输入计算机名称和有效的用户帐户名称（如<strong>MJO-DL\name@something.com</strong>）以及正确的密码。

11. 在 Visual Studio 计算机上，你应看到在断点处已停止执行。

    > [!TIP]
    > 或者，你可以采用单独的步骤部署文件。 在“解决方案资源管理器”中，右键单击“mymfc”节点，然后选择“部署”。

    如果应用程序需要非代码文件，则可以在 "**远程 Windows 调试器**" 页上的 "**要部署的其他文件**" 中指定这些文件。

    或者，你可以将文件包含在项目中，并将每个文件的 "**属性**" 页中的 " **Content** " 属性设置为 **"是"** 。 这些文件将复制到 "**远程 Windows 调试器**" 页上指定的**部署目录**。 如果需要将文件复制到**部署目录**的子文件夹，还可以将**项类型**更改为 "**复制文件**" 并指定其他属性。

## <a name="set-up-debugging-with-remote-symbols"></a>使用远程符号设置调试

[!INCLUDE [remote-debugger-symbols](../debugger/includes/remote-debugger-symbols.md)]

## <a name="see-also"></a>请参阅
- [在 Visual Studio 中进行调试](../debugger/index.yml)
- [初探调试器](../debugger/debugger-feature-tour.md)
- [配置 Windows 防火墙以便进行远程调试](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)
- [远程调试远程 IIS 计算机上的 ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)
- [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)