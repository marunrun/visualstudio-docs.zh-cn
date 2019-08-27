---
title: 远程调试在 IIS 和 Azure 上的 ASP.NET Core |Microsoft 文档
ms.custom: remotedebugging
ms.date: 05/21/2018
ms.topic: conceptual
ms.assetid: a6c04b53-d1b9-4552-a8fd-3ed6f4902ce6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
- dotnetcore
- azure
ms.openlocfilehash: 2fbdc27ba7a3ae69494bf8129e4c870f325fe621
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67824436"
---
# <a name="remote-debug-aspnet-core-on-iis-in-azure-in-visual-studio"></a>在 Visual Studio 中的 Azure 中的 IIS 上的远程调试 ASP.NET Core

本指南介绍如何设置和配置 Visual Studio ASP.NET Core 应用，将其部署到 IIS，使用 Azure，并从 Visual Studio 附加远程调试器。

在 Azure 上的远程调试的推荐的方式取决于你的方案：

* 若要调试在 Azure App Service 上的 ASP.NET Core，请参阅[调试 Azure 应用程序使用快照调试器](../debugger/debug-live-azure-applications.md)。 这是建议的方法。
* 若要调试 ASP.NET Core 上使用更加传统的调试功能的 Azure App Service，请按照本主题中的步骤 (请参阅明[在 Azure App Service 上进行远程调试](#remote_debug_azure_app_service))。

    在此方案中，必须将部署到 Azure 将应用程序从 Visual Studio，但不是需要手动安装或配置 IIS 或远程调试器 （这些组件使用虚线表示），如下图中所示。

    ![远程调试器组件](../debugger/media/remote-debugger-azure-app-service.png "Remote_debugger_components")

* 若要调试在 Azure VM 上的 IIS，请按照本主题中的步骤 (请参阅的部分[在 Azure VM 上进行远程调试](#remote_debug_azure_vm))。 这允许您使用自定义的配置的 IIS，但更复杂的安装和部署步骤。

    为 Azure VM，必须部署到 Azure 将应用程序从 Visual Studio，您还需要手动安装 IIS 角色和远程调试器下, 图中所示。

    ![远程调试器组件](../debugger/media/remote-debugger-azure-vm.png "Remote_debugger_components")

* 若要调试在 Azure Service Fabric 上的 ASP.NET Core，请参阅[调试远程 Service Fabric 应用程序](/azure/service-fabric/service-fabric-debugging-your-application#debug-a-remote-service-fabric-application)。

> [!WARNING]
> 请务必删除时的步骤完成此教程中创建的 Azure 资源。 这样可以避免产生不必要的费用。

## <a name="prerequisites"></a>系统必备

::: moniker range=">=vs-2019"
Visual Studio 2019 需按照本文中所示的步骤。
::: moniker-end
::: moniker range="vs-2017"
Visual Studio 2017 需要按照本文中所示的步骤。
::: moniker-end

### <a name="network-requirements"></a>网络要求

不支持调试通过代理连接的两台计算机之间。 调试通过高延迟或低带宽连接，例如拨号 Internet，或通过 Internet 跨国家/地区不建议并可能会失败或很令人无法接受慢。 有关要求的完整列表，请参阅[要求](../debugger/remote-debugging.md#requirements_msvsmon)。

## <a name="create-the-aspnet-core-application-on-the-visual-studio-computer"></a>在 Visual Studio 计算机上创建 ASP.NET Core 应用程序

1. 创建新的 ASP.NET Core 应用程序。

    ::: moniker range=">=vs-2019"
    在 Visual Studio 2019，键入**Ctrl + Q**若要打开搜索框中，键入**asp.net**，选择**模板**，然后选择**创建新的 ASP.NET Core Web 应用程序**. 在显示对话框中，该项目命名**MyASPApp**，然后选择**创建**。 接下来，选择**Web 应用程序 （模型-视图-控制器）** ，然后选择**创建**。
    ::: moniker-end
    ::: moniker range="vs-2017"
    在 Visual Studio 2017 中，选择**文件 > 新建 > 项目**，然后选择**Visual C# > Web > ASP.NET Core Web 应用程序**。 在 ASP.NET Core 模板部分中，选择**Web 应用程序 （模型-视图-控制器）** 。 请确保选择了 ASP.NET Core 2.1，该**启用 Docker 支持**未选中并且**身份验证**设置为**无身份验证**。 将项目命名**MyASPApp**。
    ::: moniker-end

1. 打开 About.cshtml.cs 文件，并在中设置断点`OnGet`方法 (在较旧模板中，打开 HomeController.cs 而是和中设置断点`About()`方法)。

## <a name="remote_debug_azure_app_service"></a> 在 Azure App Service 上的远程调试 ASP.NET Core

从 Visual Studio 中，可快速发布和调试你的应用的 IIS 完全预配实例。 但是，预设的 IIS 配置，并且不能自定义它。 有关详细说明，请参阅[ASP.NET Core web 应用部署到 Azure 中使用 Visual Studio](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs)。 (如果需要自定义 IIS 的功能，请尝试调试[Azure VM](#remote_debug_azure_vm)。)

#### <a name="to-deploy-the-app-and-remote-debug-using-server-explorer"></a>若要部署的应用程序和使用服务器资源管理器进行远程调试

1. 在 Visual Studio 中，右键单击项目节点并选择**发布**。

    如果先前配置了任何发布配置文件，则“发布”窗格会显示  。 单击**新的配置文件**。

1. 选择**Azure 应用服务**从**发布**对话框中，选择**新建**，并按照提示来发布。

    有关详细说明，请参阅[使用 Visual Studio 将 ASP.NET Core Web 应用部署到 Azure](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs)。

    ![发布到 Azure 应用服务](../debugger/media/remotedbg_azure_app_service_profile.png)

1. 打开**服务器资源管理器**(**视图** > **服务器资源管理器**)，应用服务实例上右键单击并选择**附加调试器**.

1. 在运行的 ASP.NET 应用程序，单击链接到**有关**页。

    应在 Visual Studio 中命中断点。

    就这么简单！ 本主题中的步骤的其余部分适用于 Azure VM 上远程调试。

## <a name="remote_debug_azure_vm"></a> 在 Azure VM 上的远程调试 ASP.NET Core

可以创建服务器的 Azure VM 的 Windows，然后安装和配置 IIS 和其他所需的软件组件。 这要花更多的时间比部署到 Azure 应用服务，要求你按照本教程中的剩余步骤。

这些服务器配置上进行了测试这些过程：
* Windows Server 2012 R2 和 IIS 8
* Windows Server 2016 和 IIS 10

### <a name="app-already-running-in-iis-on-the-azure-vm"></a>应用程序已在 IIS 中运行 Azure VM 上吗？

本文包含有关 Windows server 上的 IIS 的基本配置设置和部署该应用程序从 Visual Studio 的步骤。 这些步骤是包括在内，以确保服务器具有所需的组件安装，可以正确，运行该应用程序，您就为远程调试。

* 如果在 IIS 中运行您的应用程序，并且只是想要下载远程调试器和启动调试，请转到[下载并安装 Windows Server 上的远程工具](#BKMK_msvsmon)。

* 如果需要帮助，确保您的应用程序设置已完成，部署，并正确运行在 IIS 中，以便可以调试，请按照本主题中的所有步骤。

  * 在开始之前，请按照中所述的所有步骤[安装和运行的 IIS](/azure/virtual-machines/windows/quick-create-portal)。

  * 当网络安全组中打开端口 80 时，打开[更正端口](#bkmk_openports)远程调试器 （4024 或 4022）。 这样一来，无需以后将其打开。

### <a name="update-browser-security-settings-on-windows-server"></a>更新 Windows Server 上的浏览器安全设置

如果在 Internet Explorer （默认情况下已启用） 中启用了增强的安全配置，您可能需要将某些域添加为受信任的站点，以便可以下载某些 web 服务器组件。 添加可信的站点，通过转到**Internet 选项 > 安全性 > 受信任的站点 > 站点**。 添加以下域。

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

下载软件时，可能会显示请求授予权限以加载各种 web 站点脚本和资源。 以下一些资源不是必需的但若要简化此过程中，单击**添加**出现提示时。

### <a name="install-aspnet-core-on-windows-server"></a>在 Windows Server 上安装 ASP.NET Core

1. 在托管系统上安装 [.NET Core Windows Server 托管捆绑包](https://aka.ms/dotnetcore-2-windowshosting)。 捆绑包将安装.NET Core 运行时，.NET Core 库和 ASP.NET Core 模块。 有关更多深入说明，请参阅[发布到 IIS](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration)。

    > [!NOTE]
    > 如果系统没有 Internet 连接，请先获取并安装 [Microsoft Visual C++ 2015 Redistributable](https://www.microsoft.com/download/details.aspx?id=53840)，再安装 .NET Core Windows Server 托管捆绑包  。

3. 重启系统（或在命令提示符处依次执行“net stop was /y”和“net start w3svc”，了解系统路径的更改）   。

## <a name="choose-a-deployment-option"></a>选择部署选项

如果您需要帮助将应用部署到 IIS，请考虑这些选项：

* 通过在 IIS 中创建的发布设置文件和导入 Visual Studio 中的设置部署。 在某些情况下，这是一种将应用部署的快速方法。 创建发布设置文件时，权限自动将会在 IIS 中设置。

* 部署发布到本地文件夹并将输出的首选方法复制到 IIS 上的已准备好应用程序文件夹。

## <a name="optional-deploy-using-a-publish-settings-file"></a>（可选）使用发布设置文件进行部署

可以使用此选项创建发布设置文件，并将其导入 Visual Studio。

> [!NOTE]
> 此部署方法使用 Web 部署。 如果你想要 Web 部署手动配置 Visual Studio 中而不是导入的设置，可以为托管服务器安装 Web 部署而不是 Web 部署 3.6 3.6。 但是，如果手动配置 Web 部署，您将需要确保在服务器上的应用程序文件夹配置具有正确的值和权限 (请参阅[配置 ASP.NET Web 站点](#BKMK_deploy_asp_net))。

### <a name="install-and-configure-web-deploy-for-hosting-servers-on-windows-server"></a>安装和配置 Web 部署以便在 Windows Server 上的宿主服务器

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/install-web-deploy-with-hosting-server.md)]

### <a name="create-the-publish-settings-file-in-iis-on-windows-server"></a>在 Windows Server 上的 IIS 中创建发布设置文件

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/create-publish-settings-iis.md)]

### <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>在 Visual Studio 中导入发布设置并进行部署

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/import-publish-settings-vs.md)]

应用成功部署后，它应自动启动。 如果从 Visual Studio 不启动应用程序，请在 IIS 中启动应用程序。 对于 ASP.NET Core，需要确保将 DefaultAppPool 的应用程序池字段设置为“无托管代码”   。

1. 在中**设置**对话框中，通过单击调试启用**下一步**，选择**调试**配置，然后选择**删除其他文件目标**下**文件发布**选项。

    > [!NOTE]
    > 如果选择发布配置，则禁用在中进行调试*web.config*文件在发布时。

1. 单击**保存**然后重新发布应用程序。

## <a name="optional-deploy-by-publishing-to-a-local-folder"></a>（可选）部署发布到本地文件夹

此选项可用于部署您的应用程序，如果你想要将应用程序复制到 IIS，使用 Powershell，RoboCopy，或者想要手动复制文件。

### <a name="BKMK_deploy_asp_net"></a> Windows Server 计算机上配置 ASP.NET 网站

如果要导入发布设置，则可以跳过此部分。

1. 打开“Internet 信息服务(IIS)管理器”  并转到“站点”  。

2. 右键单击“默认网站”  节点，然后选择“添加应用程序”  。

3. 设置**别名**字段**MyASPApp**和应用程序池域**无托管代码**。 设置**物理路径**到**C:\Publish** （其中更高版本部署的 ASP.NET 项目）。

4. 在 IIS 管理器中选择站点后，选择**编辑权限**，并确保该 IUSR、 IIS_IUSRS 或配置应用程序池为授权的用户使用读取和执行权限的用户。

    如果看不到具有访问这些用户，请执行步骤将 IUSR 添加为具有读取和执行权限的用户。

### <a name="optional-publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>（可选）发布和部署应用程序通过发布到本地文件夹从 Visual Studio

如果不使用 Web 部署，必须发布和部署应用程序使用文件系统或其他工具。 您可以首先使用文件系统中，创建包，然后手动部署包或使用其他工具，例如 PowerShell、 RoboCopy 或 XCopy。 在本部分中，我们假设要手动将复制包，如果不使用 Web 部署。

[!INCLUDE [remote-debugger-deploy-app-local](../debugger/includes/remote-debugger-deploy-app-local.md)]

### <a name="BKMK_msvsmon"></a> 下载并安装 Windows Server 上的远程工具

下载与你的 Visual Studio 版本匹配远程工具的版本。

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

### <a name="BKMK_setup"></a> 设置 Windows Server 上的远程调试器

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 如果您需要添加其他用户的权限更改身份验证模式，或者远程调试器的端口号，请参阅[配置远程调试器](../debugger/remote-debugging.md#configure_msvsmon)。

### <a name="BKMK_attach"></a> 从 Visual Studio 计算机附加到 ASP.NET 应用程序

1. Visual Studio 计算机上，打开要调试的解决方案 (**MyASPApp**在您按照这篇文章中的步骤)。
2. 在 Visual Studio 中，单击**调试 > 附加到进程**（Ctrl + Alt + P）。

    > [!TIP]
    > 在 Visual Studio 2017 和更高版本中，您可以将重新附加到您以前使用附加到的同一个进程**调试 > 重新附加到进程...** (Shift + Alt + P)。

3. 将限定符字段设置为 **\<远程计算机名称>** 然后按**Enter**。

    验证 Visual Studio 将所需的端口添加到计算机名称，将出现在格式： **\<远程计算机名称>：端口**

    ::: moniker range=">=vs-2019"
    在 Visual Studio 2019，你会看到 **\<远程计算机名称>:4024**
    ::: moniker-end
    ::: moniker range="vs-2017"
    在 Visual Studio 2017 中，你会看到 **\<远程计算机名称>:4022**
    ::: moniker-end
    端口是必需的。 如果看不到的端口号，请手动添加它。

4. 单击“刷新”  。
    “可用进程”  窗口中将显示某些进程。

    如果看不到任何进程，请尝试使用的 IP 地址而不远程计算机名称 （端口是必需的）。 可以使用`ipconfig`获取 IPv4 地址的命令行中。

    如果你想要使用**查找**按钮，可能需要向[打开 UDP 端口 3702](#bkmk_openports)在服务器上。

5. 勾选“显示所有用户的进程”   。

6. 键入您的进程名称以快速查找您的应用程序的第一个字母。

    * 选择**dotnet.exe** （适用于.NET Core)

      如果有多个进程显示**dotnet.exe**，检查**用户名**列。 在某些情况下，**用户名**列显示你的应用程序池名称，如**IIS APPPOOL\DefaultAppPool**。 如果你看到应用程序池标识正确的进程的简单办法是创建一个新应用池命名为你想要调试的应用程序实例，然后您可以找到它轻松地在**用户名**列。

    * 在 IIS 某些情况下，您可能会发现你的应用名称在进程列表中，如**MyASPApp.exe**。 可以改为附加到此进程。

    ::: moniker range=">=vs-2019"
    ![RemoteDBG_AttachToProcess](../debugger/media/vs-2019/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end

7. 单击 **“附加”** 。

8. 打开远程计算机的网站。 在浏览器中，转到 http://\<remote computer name>  。

    将显示 ASP.NET 网页。
9. 在运行的 ASP.NET 应用程序，单击链接到**有关**页。

    应在 Visual Studio 中命中断点。

### <a name="bkmk_openports"></a> 故障排除：Windows Server 上打开所需的端口

在大多数系统中，所需的端口被打开的 ASP.NET 和远程调试器安装。 但是，如果你解决部署问题和应用程序托管在防火墙后面，你可能需要验证正确的端口打开。

在 Azure VM 上，则必须打开端口通过[网络安全组](/azure/virtual-machines/windows/nsg-quickstart-portal)。

所需的端口：

* 80-所需的 IIS
::: moniker range=">=vs-2019"
* 4024-所需的 Visual Studio 2019 从远程调试 (请参阅[Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)有关详细信息)。
::: moniker-end
::: moniker range="vs-2017"
* 4022 的所需的从 Visual Studio 2017 远程调试 (请参阅[Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)有关详细信息)。
::: moniker-end
* UDP 3702-（可选） 发现端口使你能够**查找**按钮时将附加到 Visual Studio 中的远程调试器。

此外，应已 ASP.NET 安装可打开这些端口：
- 8172-（可选） 所需的 Web 部署来部署该应用程序从 Visual Studio
