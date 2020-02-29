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
ms.openlocfilehash: c6a41a332e16f79673b475404af27e540689938d
ms.sourcegitcommit: 3d64bfb9bf85395357effe054db9a9afaa0be5ea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/29/2020
ms.locfileid: "78181139"
---
# <a name="remote-debug-aspnet-core-on-iis-in-azure-in-visual-studio"></a>Visual Studio 中的 Azure 上的远程调试 ASP.NET Core

本指南介绍如何设置和配置 Visual Studio ASP.NET Core 应用，如何使用 Azure 将其部署到 IIS，以及如何从 Visual Studio 附加远程调试器。

在 Azure 上进行远程调试的建议方法取决于方案：

* 若要调试 Azure App Service 上的 ASP.NET Core，请参阅[使用 Snapshot Debugger 调试 Azure 应用程序](../debugger/debug-live-azure-applications.md)。 这是建议的方法。
* 若要使用更传统的调试功能调试 Azure App Service 上的 ASP.NET Core，请按照本主题中的步骤进行操作（请参阅[Azure App Service 上的远程调试](#remote_debug_azure_app_service)部分）。

    在这种情况下，你必须将应用从 Visual Studio 部署到 Azure，但不需要手动安装或配置 IIS 或远程调试器（这些组件以虚线表示），如下图所示。

    ![远程调试器组件](../debugger/media/remote-debugger-azure-app-service.png "Remote_debugger_components")

* 若要在 Azure VM 上调试 IIS，请按照本主题中的步骤进行操作（请参阅[AZURE vm 上的远程调试](#remote_debug_azure_vm)部分）。 这样，你就可以使用 IIS 的自定义配置，但设置和部署步骤会更复杂。

    对于 Azure VM，必须将应用从 Visual Studio 部署到 Azure，并且还需要手动安装 IIS 角色和远程调试器，如下图所示。

    ![远程调试器组件](../debugger/media/remote-debugger-azure-vm.png "Remote_debugger_components")

* 若要在 Azure Service Fabric 上调试 ASP.NET Core，请参阅[调试远程 Service Fabric 应用程序](/azure/service-fabric/service-fabric-debugging-your-application#debug-a-remote-service-fabric-application)。

> [!WARNING]
> 在完成本教程中的步骤后，请确保删除你创建的 Azure 资源。 这样可以避免产生不必要的费用。

## <a name="prerequisites"></a>必备条件

::: moniker range=">=vs-2019"
若要执行本文中所述的步骤，需要安装 Visual Studio 2019。
::: moniker-end
::: moniker range="vs-2017"
若要执行本文中所述的步骤，需要安装 Visual Studio 2017。
::: moniker-end

### <a name="network-requirements"></a>网络要求

不支持在通过代理连接的两台计算机之间进行调试。 不建议在高延迟或低带宽连接（如拨号 Internet）或跨国家/地区跨 Internet 进行调试，它们可能会失败，也可能会变得很慢。 有关要求的完整列表，请参阅[要求](../debugger/remote-debugging.md#requirements_msvsmon)。

## <a name="create-the-aspnet-core-application-on-the-visual-studio-computer"></a>在 Visual Studio 计算机上创建 ASP.NET Core 应用程序

1. 创建新的 ASP.NET Core 应用程序。

    ::: moniker range=">=vs-2019"
    在 Visual Studio 2019 中，键入**Ctrl + Q**打开搜索框，键入 " **asp.net**"，选择 "**模板**"，然后选择 "**创建新的 ASP.NET Core Web 应用程序**"。 在出现的对话框中，将项目命名为**MyASPApp**，然后选择 "**创建**"。 接下来，选择 " **Web 应用程序（模型-视图-控制器）** "，然后选择 "**创建**"。
    ::: moniker-end
    ::: moniker range="vs-2017"
    在 Visual Studio 2017 中，选择 "**文件" > 新建 > 项目**"，然后选择"  **C# Visual > Web > ASP.NET Core web 应用程序**"。 在 "ASP.NET Core 模板" 部分，选择 " **Web 应用程序（模型-视图-控制器）** "。 请确保选择 "ASP.NET Core 2.1"，并选择 "**启用 Docker 支持**"，并将**身份验证**设置为 "**无身份验证**"。 将项目命名为**MyASPApp**。
    ::: moniker-end

1. 打开 About.cshtml.cs 文件并在 `OnGet` 方法中设置断点（在旧模板中，请改为打开 HomeController.cs，然后在 `About()` 方法中设置断点）。

## <a name="remote_debug_azure_app_service"></a>Azure App Service 上的远程调试 ASP.NET Core

在 Visual Studio 中，你可以快速将应用程序发布和调试到完全预配的 IIS 实例。 但是，IIS 的配置是预设的，不能对其进行自定义。 有关更多详细说明，请参阅[使用 Visual Studio 将 ASP.NET Core web 应用部署到 Azure](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs)。 （如果需要自定义 IIS 的功能，请尝试在[AZURE VM](#remote_debug_azure_vm)上进行调试。）

#### <a name="to-deploy-the-app-and-remote-debug-using-server-explorer"></a>使用服务器资源管理器部署应用和远程调试

1. 在 Visual Studio 中，右键单击项目节点，然后选择 "**发布**"。

    如果先前配置了任何发布配置文件，则“发布”窗格会显示。 单击 "**新建配置文件**"。

1. 从 "**发布**" 对话框中选择 " **Azure App Service** "，选择 "**新建**"，然后按照提示进行发布。

    有关详细说明，请参阅[使用 Visual Studio 将 ASP.NET Core Web 应用部署到 Azure](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs)。

    ![发布到 Azure 应用服务](../debugger/media/remotedbg_azure_app_service_profile.png)

1. 打开**服务器资源管理器**（**查看** > **服务器资源管理器**），右键单击应用服务实例，然后选择 "**附加调试器**"。

1. 在正在运行的 ASP.NET 应用程序中，单击 "**关于**" 页的链接。

    应在 Visual Studio 中命中断点。

    就这么简单！ 本主题中的其余步骤适用于 Azure VM 上的远程调试。

## <a name="remote_debug_azure_vm"></a>Azure VM 上的远程调试 ASP.NET Core

你可以创建适用于 Windows Server 的 Azure VM，然后安装并配置 IIS 和所需的其他软件组件。 这需要更多时间，而不是部署到 Azure App Service，要求您按照本教程中的剩余步骤进行操作。

这些过程已在以下服务器配置上进行了测试：
* Windows Server 2012 R2 和 IIS 8
* Windows Server 2016 和 IIS 10

### <a name="app-already-running-in-iis-on-the-azure-vm"></a>应用已在 Azure VM 上的 IIS 中运行？

本文包含有关在 Windows server 上设置 IIS 的基本配置以及通过 Visual Studio 部署应用程序的步骤。 包括这些步骤以确保服务器安装了所需的组件，应用程序可以正常运行，并且已准备好进行远程调试。

* 如果你的应用程序在 IIS 中运行，并且你只是想要下载远程调试器并开始调试，请参阅[下载并在 Windows Server 上安装远程工具](#BKMK_msvsmon)。

* 如果你想要帮助确保在 IIS 中正确设置、部署和运行你的应用程序以便可以进行调试，请按照本主题中的所有步骤进行操作。

  * 在开始之前，请执行[安装和运行 IIS](/azure/virtual-machines/windows/quick-create-portal)中所述的所有步骤。

  * 在网络安全组中打开端口80时，还应为远程调试器打开[正确的端口](#bkmk_openports)（4024或4022）。 这样一来，以后就不必打开它。

### <a name="update-browser-security-settings-on-windows-server"></a>更新 Windows Server 上的浏览器安全设置

如果在 Internet Explorer 中启用了增强的安全配置（默认情况下启用），则可能需要将一些域添加为受信任的站点，以便下载某些 web 服务器组件。 通过转到 " **Internet 选项" > 安全性 > 受信任的站点 > 站点**）来添加受信任的站点。 添加以下域。

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

下载软件时，你可能会收到请求，要求你授予加载各种网站脚本和资源的权限。 其中一些资源不是必需的，但为了简化此过程，请在出现提示时单击 "**添加**"。

### <a name="install-aspnet-core-on-windows-server"></a>在 Windows Server 上安装 ASP.NET Core

1. 在托管系统上安装 [.NET Core Windows Server 托管捆绑包](https://aka.ms/dotnetcore-2-windowshosting)。 捆绑包可安装 .NET Core 运行时、.NET Core 库和 ASP.NET Core 模块。 有关更深入的说明，请参阅[发布到 IIS](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration)。

    > [!NOTE]
    > 如果系统没有 Internet 连接，请先获取并安装 *Microsoft Visual C++ 2015 Redistributable[，再安装 .NET Core Windows Server 托管捆绑包](https://www.microsoft.com/download/details.aspx?id=53840)* 。

3. 重启系统（或在命令提示符处依次执行“net stop was /y”和“net start w3svc”，了解系统路径的更改）。

## <a name="choose-a-deployment-option"></a>选择部署选项

如果你需要帮助来将应用程序部署到 IIS，请考虑以下选项：

* 通过在 IIS 中创建一个发布设置文件并在 Visual Studio 中导入设置来进行部署。 在某些情况下，这是部署应用程序的快速方法。 当你创建发布设置文件时，会在 IIS 中自动设置权限。

* 通过发布到本地文件夹，然后将首选方法的输出复制到 IIS 上已准备的应用文件夹进行部署。

## <a name="optional-deploy-using-a-publish-settings-file"></a>可有可无使用发布设置文件进行部署

您可以使用此选项创建发布设置文件并将其导入到 Visual Studio 中。

> [!NOTE]
> 此部署方法使用 Web 部署。 如果要在 Visual Studio 中手动配置 Web 部署而不是导入设置，则可以安装 Web 部署3.6，而不是 Web 部署3.6 来承载服务器。 但是，如果你手动配置 Web 部署，你将需要确保使用正确的值和权限配置服务器上的应用文件夹（请参阅[configure ASP.NET 网站](#BKMK_deploy_asp_net)）。

### <a name="install-and-configure-web-deploy-for-hosting-servers-on-windows-server"></a>为 Windows Server 上的主机服务器安装和配置 Web 部署

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/install-web-deploy-with-hosting-server.md)]

### <a name="create-the-publish-settings-file-in-iis-on-windows-server"></a>在 Windows Server 上的 IIS 中创建发布设置文件

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/create-publish-settings-iis.md)]

### <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>在 Visual Studio 中导入发布设置并进行部署

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/import-publish-settings-vs.md)]

应用成功部署后，它应自动启动。 如果应用不是从 Visual Studio 启动的，请在 IIS 中启动该应用。 对于 ASP.NET Core，需要确保将 DefaultAppPool 的应用程序池字段设置为“无托管代码”。

1. 在 "**设置**" 对话框中，通过单击 "**下一步**" 启用调试，选择 "**调试**" 配置，然后选择 "**文件发布**选项" 下的 "**删除目标中的其他文件**"。

    > [!NOTE]
    > 如果选择发布配置，则在发布时 *，将在 web.config 文件中*禁用调试。

1. 单击 "**保存**"，然后重新发布应用。

## <a name="optional-deploy-by-publishing-to-a-local-folder"></a>可有可无通过发布到本地文件夹进行部署

如果要使用 PowerShell、RoboCopy 将应用复制到 IIS 或要手动复制文件，则可以使用此选项来部署应用。

### <a name="BKMK_deploy_asp_net"></a>在 Windows Server 计算机上配置 ASP.NET Core 网站

如果要导入发布设置，则可以跳过此部分。

1. 打开“Internet 信息服务(IIS)管理器” 并转到“站点”。

2. 右键单击“默认网站” 节点，然后选择“添加应用程序”。

3. 将 "**别名**" 字段设置为**MyASPApp** ，将 "应用程序池" 字段设置为 "**无托管代码**"。 将**物理路径**设置为**C:\Publish** （稍后将在其中部署 ASP.NET Core 项目）。

4. 在 IIS 管理器中选择了站点后，选择 "**编辑权限**"，并确保为应用程序池配置的 IUSR、IIS_IUSRS 或用户是具有读取 & 执行权限的授权用户。

    如果看不到这些用户的访问权限，请执行以下步骤，将 IUSR 添加为具有读取 & 执行权限的用户。

### <a name="optional-publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>可有可无通过从 Visual Studio 发布到本地文件夹来发布和部署应用

如果使用的不是 Web 部署，则必须使用文件系统或其他工具发布和部署应用。 首先，可以使用文件系统创建包，然后手动部署包，也可以使用 PowerShell、RoboCopy 或 XCopy 等其他工具。 在本部分中，我们假设你要在未使用 Web 部署的情况下手动复制包。

[!INCLUDE [remote-debugger-deploy-app-local](../debugger/includes/remote-debugger-deploy-app-local.md)]

### <a name="BKMK_msvsmon"></a>在 Windows Server 上下载和安装远程工具

下载与你的 Visual Studio 版本匹配的远程工具版本。

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

### <a name="BKMK_setup"></a>在 Windows Server 上设置远程调试器

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 如果需要添加其他用户的权限、更改身份验证模式或远程调试器的端口号，请参阅[配置远程调试器](../debugger/remote-debugging.md#configure_msvsmon)。

### <a name="BKMK_attach"></a> 从 Visual Studio 计算机附加到 ASP.NET 应用程序

1. 在 Visual Studio 计算机上，打开要调试的解决方案（如果按照本文中的步骤操作，请**MyASPApp** ）。
2. 在 Visual Studio 中，单击 "**调试" > "附加到进程**" （Ctrl + Alt + P）。

    > [!TIP]
    > 在 Visual Studio 2017 及更高版本中，可以使用 "调试" > "重新附加**到进程 ...** " （Shift + Alt + P），重新附加到以前附加到的进程。

3. 将 "限定符" 字段设置为 **\<远程计算机名称 >** ，然后按**enter**。

    验证 Visual Studio 是否向计算机名称添加所需的端口，该端口采用以下格式： **\<远程计算机名称 >:p o**

    ::: moniker range=">=vs-2019"
    在 Visual Studio 2019 上，应看到 **\<远程计算机名称 >： 4024**
    ::: moniker-end
    ::: moniker range="vs-2017"
    在 Visual Studio 2017 上，应看到 **\<远程计算机名称 >： 4022**
    ::: moniker-end
    端口是必需的。 如果看不到端口号，请手动添加。

4. 单击“刷新”。
    “可用进程” 窗口中将显示某些进程。

    如果看不到任何进程，请尝试使用 IP 地址而不是远程计算机名称（端口是必需的）。 可以在命令行中使用 `ipconfig` 来获取 IPv4 地址。

    如果要使用 "**查找**" 按钮，可能需要在服务器上[打开 UDP 端口 3702](#bkmk_openports) 。

5. 勾选“显示所有用户的进程”。

6. 键入你的进程名称的第一个字母，以快速查找你的应用。

    * 选择**dotnet** （适用于 .net Core）

      如果有多个显示**dotnet**的进程，请检查 "**用户名**" 列。 在某些情况下，"**用户名**" 列会显示应用池名称，如**IIS APPPOOL\DefaultAppPool**。 如果你看到应用程序池，则可以使用一种简单的方法来确定正确的进程：为要调试的应用程序实例创建新的命名应用程序池，然后在 "**用户名**" 列中轻松找到它。

    * 在某些 IIS 方案中，你可能会在进程列表中找到你的应用程序名称，例如**MyASPApp**。 您可以改为附加到此进程。

    ::: moniker range=">=vs-2019"
    ![RemoteDBG_AttachToProcess](../debugger/media/vs-2019/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end

7. 单击 **“附加”** 。

8. 打开远程计算机的网站。 在浏览器中，转到 http://**remote computer name>\<** 。

    将显示 ASP.NET 网页。
9. 在正在运行的 ASP.NET 应用程序中，单击 "**关于**" 页的链接。

    应在 Visual Studio 中命中断点。

### <a name="bkmk_openports"></a> 疑难解答Windows Server 上打开所需的端口

在大多数情况下，所需的端口都是通过安装 ASP.NET 和远程调试器打开的。 但是，如果您正在排查部署问题，而且该应用程序托管在防火墙后面，则您可能需要验证是否打开了正确的端口。

在 Azure VM 上，必须通过[网络安全组](/azure/virtual-machines/windows/nsg-quickstart-portal)打开端口。

所需端口：

* 80-IIS 需要
::: moniker range=">=vs-2019"
* 4024-从 Visual Studio 2019 进行远程调试需要此项（有关详细信息，请参阅[远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)）。
::: moniker-end
::: moniker range="vs-2017"
* 4022-从 Visual Studio 2017 进行远程调试需要此项（有关详细信息，请参阅[远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)）。
::: moniker-end
* 当附加到 Visual Studio 中的远程调试器时，UDP 3702-（可选）发现端口可用于 "**查找**" 按钮。

此外，ASP.NET 安装还应打开这些端口：
- 8172-（可选）从 Visual Studio 部署应用时需要 Web 部署
