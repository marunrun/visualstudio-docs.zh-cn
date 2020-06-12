---
title: IIS 和 Azure 上的远程调试 ASP.NET Core |Microsoft Docs
ms.custom: remotedebugging
ms.date: 05/06/2020
ms.topic: conceptual
ms.assetid: a6c04b53-d1b9-4552-a8fd-3ed6f4902ce6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
- dotnetcore
- azure
ms.openlocfilehash: 6983d3ac191b8eb85d38e1d40afa3244e97dbb17
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84184245"
---
# <a name="remote-debug-aspnet-core-on-iis-in-azure-in-visual-studio"></a>在 Azure 中的 IIS 上的 Visual Studio 中远程调试 ASP.NET Core

本指南说明如何设置和配置 Visual Studio ASP.NET Core 应用，使用 Azure 将其部署到 IIS，并从 Visual Studio 附加远程调试器。

在 Azure 上进行远程调试的建议方法取决于具体场景：

* 若要调试 Azure 应用服务上的 ASP.NET Core，请参阅[使用 Snapshot Debugger 调试 Azure 应用](../debugger/debug-live-azure-applications.md)。 这是建议的方法。
* 若要使用更传统的调试功能调试 Azure应用服务上的 ASP.NET Core，请按照本主题中的步骤进行操作（请参阅 [Azure 应用服务上的远程调试](#remote_debug_azure_app_service)一节）。

    在这种情况下，必须将应用从 Visual Studio 部署到 Azure，但不需要手动安装或配置 IIS 或远程调试器（这些组件以虚线表示），如下图所示。

    ![远程调试器组件](../debugger/media/remote-debugger-azure-app-service.png "Remote_debugger_components")

* 若要在 Azure VM 上调试 IIS，请按照本主题中的步骤进行操作（请参阅 [Azure VM 上的远程调试](#remote_debug_azure_vm)一节）。 这样就可以使用 IIS 的自定义配置，但设置和部署步骤会更复杂。

    对于 Azure VM，必须将应用从 Visual Studio 部署到 Azure，并且还需要手动安装 IIS 角色和远程调试器，如下图所示。

    ![远程调试器组件](../debugger/media/remote-debugger-azure-vm.png "Remote_debugger_components")

* 若要调试 Azure Service Fabric 上的 ASP.NET，请参阅[调试远程 Service Fabric 应用程序](/azure/service-fabric/service-fabric-debugging-your-application#debug-a-remote-service-fabric-application)。

> [!WARNING]
> 在完成本教程中的步骤后，请确保删除你创建的 Azure 资源。 这样可以避免产生不必要的费用。

## <a name="prerequisites"></a>先决条件

::: moniker range=">=vs-2019"
需要安装 Visual Studio 2019 才能执行本文所述的步骤。
::: moniker-end
::: moniker range="vs-2017"
需要安装 Visual Studio 2017 才能执行本文所述的步骤。
::: moniker-end

### <a name="network-requirements"></a>网络要求

不支持在通过代理连接的两台计算机之间进行调试。 不建议通过高延迟或低带宽连接（如拨号 Internet）或跨国家/地区的 Internet 进行调试，否则可能会导致调试失败或速度过慢。 有关要求的完整列表，请参阅[要求](../debugger/remote-debugging.md#requirements_msvsmon)。

## <a name="create-the-aspnet-core-application-on-the-visual-studio-computer"></a>在 Visual Studio 计算机上创建 ASP.NET Core 应用程序

1. 创建新的 ASP.NET Core 应用程序。

    ::: moniker range=">=vs-2019"
    在 Visual Studio 2019 中，键入 Ctrl + Q 打开搜索框，键入“asp.net”，选择“模板”，然后选择“创建新的 ASP.NET Core Web 应用程序”   。 在出现的对话框中，将项目命名为“MyASPApp”，然后选择“创建” 。 接下来，选择“Web 应用程序(模型-视图-控制器)”，然后选择“创建” 。
    ::: moniker-end
    ::: moniker range="vs-2017"
    在 Visual Studio 2017 中，选择“文件”>“新建”>“项目”，然后选择“Visual C#”>“Web”>“ASP.NET Core Web 应用程序” 。 在“ASP.NET Core 模板”部分中，选择“Web 应用程序(模型-视图-控制器)”。 确保选择了 ASP.NET Core 2.1，未选择“启用 Docker 支持”，并且“身份验证”设置为“无身份验证”  。 将项目命名为“MyASPApp”。
    ::: moniker-end

1. 打开 About.cshtml.cs 文件，并在 `OnGet` 方法中设置断点（在较旧的模板中，改为打开 HomeController.cs 并在 `About()` 方法中设置断点）。

## <a name="remote-debug-aspnet-core-on-an-azure-app-service"></a><a name="remote_debug_azure_app_service"></a>远程调试 Azure 应用服务上的 ASP.NET Core

在 Visual Studio 中，你可以快速将应用发布和调试为完全预配的 IIS 实例。 但是，IIS 的配置是预设的，不能对其进行自定义。 有关详细说明，请参阅[使用 Visual Studio 将 ASP.NET Core Web 应用部署到 Azure](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs)。 （如果需要自定义 IIS，请尝试在 [Azure VM](#remote_debug_azure_vm) 上进行调试。）

#### <a name="to-deploy-the-app-and-remote-debug-using-cloud-explorer"></a>使用 Cloud Explorer 部署应用和远程调试

1. 在 Visual Studio 中，右键单击项目节点，然后选择“发布”。

    如果先前配置了任何发布配置文件，则“发布”窗格会显示。 单击“新建配置文件”。

1. 从“发布”对话框中选择“Azure 应用服务”，选择“新建”并按照提示创建配置文件  。

    有关详细说明，请参阅[使用 Visual Studio 将 ASP.NET Core Web 应用部署到 Azure](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs)。

    ![发布到 Azure 应用服务](../debugger/media/remotedbg_azure_app_service_profile.png)

1. 在“发布”窗口中，选择“编辑配置”然后切换到“调试”配置，然后选择“发布” 。

   调试应用需要“调试”配置。

1. 打开“Cloud Explorer”（“视图” > “Cloud Explorer”），右键单击应用服务实例，然后选择“附加调试器”   。

   如果 Cloud Explorer 不可用，则改为打开服务器资源管理器。 然后右键单击服务器资源管理器中的应用服务实例，选择“附加调试器”。

1. 在正在运行的 ASP.NET 应用程序中，单击指向“关于”页面的链接。

    应在 Visual Studio 中命中断点。

    就这么简单！ 本主题中的其余步骤适用于 Azure VM 上的远程调试。

## <a name="remote-debug-aspnet-core-on-an-azure-vm"></a><a name="remote_debug_azure_vm"></a> 远程调试 Azure VM 上的 ASP.NET Core

可以创建适用于 Windows Server 的 Azure VM，然后安装并配置 IIS 和所需的其他软件组件。 这比部署到 Azure 应用服务需要更多时间，并且需要按照本教程中的剩余步骤进行操作。

这些过程已在以下服务器配置上进行了测试：
* Windows Server 2012 R2 和 IIS 8
* Windows Server 2016 和 IIS 10
* Windows Server 2019 和 IIS 10

### <a name="app-already-running-in-iis-on-the-azure-vm"></a>应用已在 Azure VM 上的 IIS 中运行？

本文包含有关在 Windows Server 上设置 IIS 的基本配置以及从 Visual Studio 部署应用的步骤。 这些步骤可确保服务器安装了必需的组件，应用可以正常运行，以及你已经准备好进行远程调试。

* 如果应用正在 IIS 中运行，你只想下载远程调试器并启动调试，请转到[在 Windows Server 上下载并安装远程工具](#BKMK_msvsmon)。

* 如果需要帮助确保在 IIS 中正确设置、部署和运行应用，以便进行调试，请按照本主题中的所有步骤进行操作。

  * 在开始之前，请按照[安装和运行 IIS](/azure/virtual-machines/windows/quick-create-portal) 中所述的所有步骤进行操作。

  * 在网络安全组中打开端口 80 时，还应为远程调试器打开[正确的端口](#bkmk_openports)（4024 或 4022）。 这样一来，以后就不必打开它。 如果使用的是 Web 部署，还应打开端口 8172。

### <a name="update-browser-security-settings-on-windows-server"></a>更新 Windows Server 上的浏览器安全设置

如果在 Internet Explorer 中启用了“增强的安全配置”（默认情况下已启用），则可能需要将某些域添加为受信任的站点，以便下载某些 Web 服务器组件。 通过转到“Internet 选项”>“安全性”>“受信任的站点”>“站点”来添加受信任的站点。 添加以下域。

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

下载软件时，可能会收到授权加载各种网站脚本和资源的请求。 其中一些资源不是必需的，但为了简化此过程，请在出现提示时单击“添加”。

### <a name="install-aspnet-core-on-windows-server"></a>在 Windows Server 上安装 ASP.NET Core

1. 在托管系统上安装 .NET Core 托管捆绑包。 捆绑包可安装 .NET Core 运行时、.NET Core 库和 ASP.NET Core 模块。 有关更深入的说明，请参阅[发布到 IIS](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration)。

    对 .NET Core 3，安装 [.NET Core 托管捆绑包](https://dotnet.microsoft.com/permalink/dotnetcore-current-windows-runtime-bundle-installer)。
    对 .NET Core 2，安装 [.NET Core Windows Server 托管捆绑包](https://aka.ms/dotnetcore-2-windowshosting)。

    > [!NOTE]
    > 如果系统没有 Internet 连接，请先获取并安装 [Microsoft Visual C++ 2015 Redistributable](https://www.microsoft.com/download/details.aspx?id=53840)，再安装 .NET Core Windows Server 托管捆绑包。

3. 重启系统（或在命令提示符处依次执行“net stop was /y”和“net start w3svc”，了解系统路径的更改） 。

## <a name="choose-a-deployment-option"></a>选择部署选项

如果需要帮助将应用部署到 IIS，请考虑以下选项：

* 通过在 IIS 中创建发布设置文件并在 Visual Studio 中导入设置来进行部署。 在某些情况下，这是一种快速部署应用的方法。 当你创建发布设置文件时，系统会在 IIS 中自动设置权限。

* 通过发布到本地文件夹并使用首选方法将输出复制到 IIS 上准备就绪的应用文件夹来进行部署。

## <a name="optional-deploy-using-a-publish-settings-file"></a>（可选）使用发布设置文件进行部署

可以使用此选项创建一个发布设置文件，并将其导入到 Visual Studio 中。

> [!NOTE]
> 此部署方法使用 Web 部署，必须安装在服务器上。 如果要手动配置 Web 部署，而不是导入设置，则可以安装 Web 部署 3.6，而不是用于托管服务器的 Web 部署 3.6。 但是，如果手动配置 Web 部署，则需要确保使用正确的值和权限配置服务器上的应用文件夹（请参阅[配置 ASP.NET 网站](#BKMK_deploy_asp_net)）。

### <a name="configure-the-aspnet-core-web-site"></a>配置 ASP.NET Core 网站

1. 在 IIS 管理器左窗格的“连接”下，选择“应用程序池” 。 打开 DefaultAppPool，将“.NET CLR 版本”设置为“无托管代码”  。 ASP.NET Core 需要执行此操作。 默认网站使用 DefaultAppPool。

2. 停止并重新启动 DefaultAppPool。

### <a name="install-and-configure-web-deploy-for-hosting-servers-on-windows-server"></a>在 Windows Server 上安装和配置用于宿主服务器的 Web 部署

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/install-web-deploy-with-hosting-server.md)]

### <a name="create-the-publish-settings-file-in-iis-on-windows-server"></a>在 Windows Server 上的 IIS 中创建发布设置文件

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/create-publish-settings-iis.md)]

### <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>在 Visual Studio 中导入发布设置并进行部署

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/import-publish-settings-vs.md)]

    > [!NOTE]
    > If you restart an Azure VM, the IP address may change.

应用成功部署后，它应自动启动。 如果在 Visual Studio 中无法启动应用，请在 IIS 中启动应用以验证其是否正常运行。 对于 ASP.NET Core，还需要确保将 DefaultAppPool 的“应用程序池”字段设置为“无托管代码” 。

1. 在“设置”对话框中，单击“下一步”启用调试，选择“调试”配置，然后在“文件发布”选项下选择“删除目标处的其他文件”    。

    > [!IMPORTANT]
    > 如果选择发布配置，则在发布时，需要在 web.config 文件中禁用调试。

1. 单击“保存”，然后重新发布应用。

## <a name="optional-deploy-by-publishing-to-a-local-folder"></a>（可选）通过发布到本地文件夹进行部署

如果要使用 PowerShell、RoboCopy 将应用复制到 IIS，或者要手动复制文件，则可以使用此选项来部署应用。

### <a name="configure-the-aspnet-core-web-site-on-the-windows-server-computer"></a><a name="BKMK_deploy_asp_net"></a> 在 Windows Server 计算机上配置 ASP.NET Core 网站

如果要导入发布设置，则可以跳过此部分。

1. 打开“Internet 信息服务(IIS)管理器”  并转到“站点” 。

2. 右键单击“默认网站”  节点，然后选择“添加应用程序” 。

3. 将“别名”字段设置为“MyASPApp”并将应用程序池字段设置为“无托管代码”  。 将“物理路径”设置为 C:\Publish（稍后部署 ASP.NET Core 项目的位置） 。

4. 在 IIS 管理器中选择了站点后，选择“编辑权限”，并确保为应用程序池配置的 IUSR、IIS_IUSRS 或用户是拥有读取和执行权限的授权用户。

    如果没有看到其中任何一个用户具有访问权限，请执行相应步骤将 IUSR 添加为具有读取和执行权限的用户。

### <a name="optional-publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>（可选）通过从 Visual Studio 发布到本地文件夹来发布和部署应用

如果未使用 Web 部署，则必须使用文件系统或其他工具发布和部署应用。 首先可以使用文件系统创建包，然后手动部署包，也可以使用 PowerShell、RoboCopy 或 XCopy 等其他工具。 在本部分中，假设你要在不使用 Web 部署的情况下手动复制包。

[!INCLUDE [remote-debugger-deploy-app-local](../debugger/includes/remote-debugger-deploy-app-local.md)]

### <a name="download-and-install-the-remote-tools-on-windows-server"></a><a name="BKMK_msvsmon"></a>在 Windows Server 上下载并安装远程工具

下载与 Visual Studio 版本匹配的远程工具版本。

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

### <a name="set-up-the-remote-debugger-on-windows-server"></a><a name="BKMK_setup"></a>在 Windows Server 上设置远程调试器

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 如果需要为其他用户添加权限，请更改远程调试器的身份验证模式或端口号，请参阅[配置远程调试器](../debugger/remote-debugging.md#configure_msvsmon)。

### <a name="attach-to-the-aspnet-application-from-the-visual-studio-computer"></a><a name="BKMK_attach"></a> 从 Visual Studio 计算机附加到 ASP.NET 应用程序

1. 在 Visual Studio 计算机上，打开尝试调试的解决方案（如果按照本文中的步骤操作，则是 MyASPApp）。
2. 在 Visual Studio 中，单击“调试”>“附加到进程”(Ctrl + Alt + P)。

    > [!TIP]
    > 在 Visual Studio 2017 及更高版本中，可以使用“调试”>“重新附加到进程...”重新附加到以前附加的相同进程(Shift+Alt+P)。

3. 将限定符字段设置为 \<remote computer name>，并按 Enter 。

    确保 Visual Studio 将所需的端口添加到计算机名称中，其格式为：\<remote computer name>:port

    ::: moniker range=">=vs-2019"
    在 Visual Studio 2019 中应看到 \<remote computer name>:4024
    ::: moniker-end
    ::: moniker range="vs-2017"
    在 Visual Studio 2017 中应看到 \<remote computer name>:4022
    ::: moniker-end
    端口是必需的。 如果看不到端口号，请手动添加。

4. 单击“刷新”。
    “可用进程”  窗口中将显示某些进程。

    如果看不到任何进程，请尝试使用 IP 地址而不是远程计算机名称（端口是必需的）。 可以在命令行中使用 `ipconfig` 来获取 IPv4 地址。

    如果要使用“查找”按钮，则可能需要在服务器上[打开 UDP 端口 3702](#bkmk_openports)。

5. 勾选“显示所有用户的进程”  。

6. 键入进程名称的第一个字母，以快速查找应用。

    * 如果正在 IIS 上使用[进程内托管模型](/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-3.1#hosting-models)，请选择正确的 w3wp.exe 进程。 从 .NET Core 3 开始，这是默认设置。

    * 否则，请选择 dotnet.exe 进程。 （这是进程外托管模型。）

    如果有多个进程显示 w3wp.exe 或 dotnet.exe，请检查“用户名”列。 在某些情况下，“用户名”列显示应用池名称，例如 IIS APPPOOL\DefaultAppPool。 如果你看到了应用池，但它不是唯一的，则为要调试的应用实例创建一个使用新名称的应用池，然后就可以在“用户名”列中轻松找到它了。

    ::: moniker range=">=vs-2019"
    ![RemoteDBG_AttachToProcess](../debugger/media/vs-2019/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end

7. 单击 **“附加”** 。

8. 打开远程计算机的网站。 在浏览器中，转到 http://\<remote computer name>。

    将显示 ASP.NET 网页。
9. 在正在运行的 ASP.NET 应用程序中，单击指向“关于”页面的链接。

    应在 Visual Studio 中命中断点。

### <a name="troubleshooting-open-required-ports-on-windows-server"></a><a name="bkmk_openports"></a> 排除故障：在 Windows Server 上打开必需端口

在大多数设置中，必需端口通过安装 ASP.NET 和远程调试器来打开。 但是，如果正在排查部署问题，而且应用受防火墙保护，则你可能需要验证是否打开了正确的端口。

在 Azure VM 上，必须通过[网络安全组](/azure/virtual-machines/windows/nsg-quickstart-portal)打开端口。

必需端口：

* 80 - 对于 IIS 是必需的
::: moniker range=">=vs-2019"
* 4024 - 从 Visual Studio 2019 进行远程调试时必需（有关详细信息，请参阅[远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)）。
::: moniker-end
::: moniker range="vs-2017"
* 4022 - 从 Visual Studio 2017 进行远程调试时必需（有关详细信息，请参阅[远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)）。
::: moniker-end
* UDP 3702 -（可选）发现端口允许你在附加到 Visual Studio 中的远程调试器时使用“查找”按钮。

此外，安装 ASP.NET 后应该就打开了这些端口：
- 8172 -（可选）使用 Web 部署从 Visual Studio 部署应用时必需
