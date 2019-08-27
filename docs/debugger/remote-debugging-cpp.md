---
title: 远程调试视觉对象C++项目 |Microsoft Docs
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
ms.openlocfilehash: fbfdb246769ac55afd7f164d91673e39e293f4c4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62903491"
---
# <a name="remote-debugging-a-visual-c-project-in-visual-studio"></a>远程调试视觉对象C++Visual Studio 项目中
若要调试在另一台计算机上的 Visual Studio 应用程序、 安装和将在其中部署您的应用程序的计算机上运行远程工具，将项目配置为从 Visual Studio 中，连接到远程计算机然后部署并运行你的应用。

![远程调试器组件](../debugger/media/remote-debugger-client-apps.png "Remote_debugger_components")

有关远程调试通用 Windows 应用 (UWP) 的信息，请参阅[调试安装的应用程序包](debug-installed-app-package.md)。

## <a name="requirements"></a>要求

远程调试器是在 Windows 7 上受支持和更高版本 (不 phone) 和从 Windows Server 2008 Service Pack 2 的 Windows Server 的版本。 有关要求的完整列表，请参阅[要求](../debugger/remote-debugging.md#requirements_msvsmon)。

> [!NOTE]
> 不支持调试通过代理连接的两台计算机之间。 调试通过高延迟或低带宽连接，例如拨号 Internet，或通过 Internet 跨国家/地区不建议并可能会失败或很令人无法接受慢。

## <a name="download-and-install-the-remote-tools"></a>下载和安装远程工具

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

> [!TIP]
> 在某些情况下，它可以是最有效，若要从文件共享运行远程调试器。 有关详细信息，请参阅[从文件共享运行远程调试器](../debugger/remote-debugging.md#fileshare_msvsmon)。

## <a name="BKMK_setup"></a>设置远程调试器

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 如果您需要添加其他用户的权限更改身份验证模式，或者远程调试器的端口号，请参阅[配置远程调试器](../debugger/remote-debugging.md#configure_msvsmon)。

## <a name="remote_cplusplus"></a> 远程调试 Visual C++ 项目
 在下面的过程的名称和项目的路径是 C:\remotetemp\MyMfc，且远程计算机的名称是**MJO DL**。

1. 创建名为 mymfc 的 MFC 应用程序。

2. 在应用程序中容易到达的地方设置断点，例如，在 MainFrm.cpp 中（位于 `CMainFrame::OnCreate` 的开头）。

3. 在解决方案资源管理器中右键单击项目并选择**属性**。 打开“调试”选项卡。

4. 将“要启动的调试器”更改为“远程 Windows 调试器”。

    ![RemoteDebuggingCPlus](../debugger/media/remotedebuggingcplus.png "RemoteDebuggingCPlus")

5. 对属性进行以下更改：

   |设置|“值”|
   |-|-|
   |远程命令|C:\remotetemp\mymfc.exe|
   |工作目录|C:\remotetemp|
   |远程服务器名称|MJO DL:*端口号*|
   |连接|带 Windows 身份验证的远程访问|
   |调试器类型|仅限本机|
   |部署目录|C:\remotetemp。|
   |其他要部署的文件|C:\data\mymfcdata.txt。|

    如果你部署其他文件 （可选），该文件夹必须存在两台计算机上。

6. 在解决方案资源管理器，右键单击解决方案并选择**Configuration Manager**。

7. 对于“调试”配置，请选中“部署”复选框。

    ![RemoteDebugCplusDeploy](../debugger/media/remotedebugcplusdeploy.png "RemoteDebugCplusDeploy")

8. 开始调试（单击“调试”>“启动调试”，或按 F5）。

9. 可执行文件会自动部署到远程计算机。

10. 如果系统提示，请输入网络凭据以连接到远程计算机。

     特定于网络的安全配置所需的凭据。 例如，可能的域计算机上，选择安全证书或输入你的域名和密码。 在非域计算机上，你可能会输入计算机名称和有效的用户帐户名称，如<strong>MJO-DL\name@something.com</strong>，以及正确的密码。

11. 在 Visual Studio 计算机上，你应看到在断点处已停止执行。

    > [!TIP]
    > 或者，你可以采用单独的步骤部署文件。 在“解决方案资源管理器”中，右键单击“mymfc”节点，然后选择“部署”。

    如果具有所需的应用程序的非代码文件，则可以指定在**其他文件复制到部署**上**远程 Windows 调试器**页。

    或者，可以在项目中包括的文件，并设置**内容**属性设置为**是**中**属性**页为每个文件。 这些文件复制到**部署目录**中所指定**远程 Windows 调试器**页。 此外可以更改**项类型**到**复制文件**，如果您需要的文件复制到的子文件夹指定其他属性那里**部署目录**。

## <a name="set-up-debugging-with-remote-symbols"></a>使用远程符号设置调试

[!INCLUDE [remote-debugger-symbols](../debugger/includes/remote-debugger-symbols.md)]

## <a name="see-also"></a>请参阅
- [在 Visual Studio 中进行调试](../debugger/index.md)
- [初探调试器](../debugger/debugger-feature-tour.md)
- [配置 Windows 防火墙以便进行远程调试](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)
- [远程调试远程 IIS 计算机上的 ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)
- [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)