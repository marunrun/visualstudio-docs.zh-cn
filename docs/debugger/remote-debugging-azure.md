---
title: IIS 和 Azure 上的远程调试ASP.NET核心 |微软文档
ms.custom: remotedebugging
ms.date: 04/14/2020
ms.topic: conceptual
ms.assetid: a6c04b53-d1b9-4552-a8fd-3ed6f4902ce6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
- dotnetcore
- azure
ms.openlocfilehash: 079e324f2304118c9041118c13e8ebc0cce2015c
ms.sourcegitcommit: cc58ca7ceae783b972ca25af69f17c9f92a29fc2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "81385498"
---
# <a name="remote-debug-aspnet-core-on-iis-in-azure-in-visual-studio"></a>远程调试ASP.NET可视化工作室中 Azure 中的 IIS 核心

本指南介绍如何设置和配置 Visual Studio ASP.NET核心应用，使用 Azure 将其部署到 IIS，以及从 Visual Studio 附加远程调试器。

建议在 Azure 上远程调试的方法取决于您的方案：

* 要在 Azure 应用服务上调试 ASP.NET 核心，请参阅[使用快照调试器 调试 Azure 应用](../debugger/debug-live-azure-applications.md)。 这是建议的方法。
* 要使用更传统的调试功能调试 Azure 应用服务上的 ASP.NET 核心，请按照本主题中的步骤操作（请参阅[Azure 应用服务上的"远程调试](#remote_debug_azure_app_service)"部分）。

    在这种情况下，必须将应用从 Visual Studio 部署到 Azure，但无需手动安装或配置 IIS 或远程调试器（这些组件以虚线表示），如下图所示。

    ![远程调试器组件](../debugger/media/remote-debugger-azure-app-service.png "Remote_debugger_components")

* 要在 Azure VM 上调试 IIS，请按照本主题中的步骤操作（请参阅[Azure VM 上的"远程调试"部分](#remote_debug_azure_vm)）。 这允许您使用自定义的 IIS 配置，但设置和部署步骤更为复杂。

    对于 Azure VM，必须将应用从 Visual Studio 部署到 Azure，并且还需要手动安装 IIS 角色和远程调试器，如下图所示。

    ![远程调试器组件](../debugger/media/remote-debugger-azure-vm.png "Remote_debugger_components")

* 要在 Azure 服务结构上调试ASP.NET核心，请参阅[调试远程服务结构应用程序](/azure/service-fabric/service-fabric-debugging-your-application#debug-a-remote-service-fabric-application)。

> [!WARNING]
> 请务必删除完成本教程中的步骤后创建的 Azure 资源。 这样，您就可以避免产生不必要的费用。

## <a name="prerequisites"></a>先决条件

::: moniker range=">=vs-2019"
Visual Studio 2019 需要遵循本文中所示的步骤。
::: moniker-end
::: moniker range="vs-2017"
Visual Studio 2017 需要遵循本文中所示的步骤。
::: moniker-end

### <a name="network-requirements"></a>网络要求

不支持在通过代理连接的两台计算机之间进行调试。 不建议通过高延迟或低带宽连接（如拨号 Internet）或跨国家/地区的 Internet 进行调试，并且可能会失败或速度过慢，令人无法接受。 有关需求的完整列表，请参阅[要求](../debugger/remote-debugging.md#requirements_msvsmon)。

## <a name="create-the-aspnet-core-application-on-the-visual-studio-computer"></a>在可视化工作室计算机上创建ASP.NET核心应用程序

1. 创建新ASP.NET核心应用程序。

    ::: moniker range=">=vs-2019"
    在 Visual Studio 2019 中，键入**Ctrl + Q**以打开搜索框，键入**asp.net，** 选择**模板**，然后选择**创建新ASP.NET核心 Web 应用程序**。 在显示的对话框中，为项目**MyASApp**命名 ，然后选择"**创建**"。 接下来，选择**Web 应用程序（模型视图控制器），** 然后选择 **"创建**"。
    ::: moniker-end
    ::: moniker range="vs-2017"
    在 Visual Studio 2017 中，选择 **"文件>新的>项目**，然后选择**Visual C# > Web >ASP.NET核心 Web 应用程序**。 在"ASP.NET核心模板部分中，选择**Web 应用程序（模型-视图控制器）**。 请确保选择了ASP.NET核心 2.1，未选择**启用 Docker 支持**，并且**身份验证**设置为 **"无身份验证**"。 命名项目**MyASApp**。
    ::: moniker-end

1. 打开About.cshtml.cs文件并在`OnGet`方法中设置断点（在较旧的模板中，改为打开HomeController.cs并在`About()`方法中设置断点）。

## <a name="remote-debug-aspnet-core-on-an-azure-app-service"></a><a name="remote_debug_azure_app_service"></a>Azure 应用服务上的远程调试ASP.NET核心

在 Visual Studio 中，您可以快速将应用发布到完全预配的 IIS 实例，并将应用调试到完全预配的 IIS 实例。 但是，IIS 的配置是预设的，您不能对其进行自定义。 有关更详细的说明，请参阅使用[Visual Studio 将ASP.NET核心 Web 应用部署到 Azure。](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs) （如果需要自定义 IIS 的能力，请尝试在[Azure VM](#remote_debug_azure_vm)上进行调试。

#### <a name="to-deploy-the-app-and-remote-debug-using-cloud-explorer"></a>使用云资源管理器部署应用和远程调试

1. 在可视化工作室中，右键单击项目节点并选择 **"发布**"。

    如果先前配置了任何发布配置文件，则“发布”窗格会显示****。 单击 **"新配置文件**"。

1. 从 **"发布"** 对话框中选择**Azure 应用服务**，选择 **"新建**"，然后按照提示创建配置文件。

    有关详细说明，请参阅[使用 Visual Studio 将 ASP.NET Core Web 应用部署到 Azure](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs)。

    ![发布到 Azure 应用服务](../debugger/media/remotedbg_azure_app_service_profile.png)

1. 在"发布"窗口中，选择 **"编辑配置"** 并切换到调试配置，然后选择 **"发布**"。

   调试应用需要调试配置。

1. 开放**云资源管理器**（**查看** > **云资源管理器**），右键单击应用服务实例并选择**附加调试器**。

   如果云资源管理器不可用，则改为打开服务器资源管理器。 然后，右键单击服务器资源管理器中的应用服务实例，然后选择**附加调试器**。

1. 在正在运行的ASP.NET应用程序中，单击指向 **"关于"** 页面的链接。

    应在 Visual Studio 中命中断点。

    就这么简单！ 本主题中的其他步骤将应用于 Azure VM 上的远程调试。

## <a name="remote-debug-aspnet-core-on-an-azure-vm"></a><a name="remote_debug_azure_vm"></a>Azure VM 上的远程调试ASP.NET核心

可以为 Windows 服务器创建 Azure VM，然后安装和配置 IIS 和其他必需的软件组件。 这比部署到 Azure 应用服务所花费的时间要长，并且需要遵循本教程中的其余步骤。

这些过程已在以下服务器配置上过测试：
* Windows 服务器 2012 R2 和 IIS 8
* Windows 服务器 2016 和 IIS 10

### <a name="app-already-running-in-iis-on-the-azure-vm"></a>已在 Azure VM 上的 IIS 中运行的应用？

本文包括有关在 Windows 服务器上设置 IIS 的基本配置和从 Visual Studio 部署应用的步骤。 包括这些步骤，以确保服务器安装了所需的组件，应用可以正常运行，并且您已准备好进行远程调试。

* 如果你的应用在 IIS 中运行，并且只想下载远程调试器并开始调试，请转到 Windows[服务器上下载并安装远程工具](#BKMK_msvsmon)。

* 如果希望帮助确保应用在 IIS 中设置、部署和正确运行，以便可以调试，请按照本主题中的所有步骤操作。

  * 在开始之前，请按照安装中描述的所有步骤[操作并运行 IIS](/azure/virtual-machines/windows/quick-create-portal)。

  * 在网络安全组中打开端口 80 时，还会打开远程调试器 （4024 或 4022）[的正确端口](#bkmk_openports)。 这样，您就不必稍后打开它了。

### <a name="update-browser-security-settings-on-windows-server"></a>更新 Windows 服务器上的浏览器安全设置

如果在 Internet 资源管理器中启用了增强的安全配置（默认情况下已启用），则可能需要将某些域添加为受信任的站点，以便能够下载某些 Web 服务器组件。 通过访问**互联网选项>安全>受信任网站>网站**添加受信任的网站。 添加以下域。

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

下载软件时，您可能会收到请求，请求授予加载各种网站脚本和资源的权限。 其中一些资源不是必需的，但为了简化该过程，请在提示时单击 **"添加**"。

### <a name="install-aspnet-core-on-windows-server"></a>在 Windows 服务器上安装 ASP.NET 核心

1. 在托管系统上安装 [.NET Core Windows Server 托管捆绑包](https://aka.ms/dotnetcore-2-windowshosting)。 捆绑包可安装 .NET Core 运行时、.NET Core 库和 ASP.NET Core 模块。 有关更深入的说明，请参阅[发布到 IIS](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration)。

    > [!NOTE]
    > 如果系统没有 Internet 连接，请先获取并安装 [Microsoft Visual C++ 2015 Redistributable](https://www.microsoft.com/download/details.aspx?id=53840)，再安装 .NET Core Windows Server 托管捆绑包**。

3. 重启系统（或在命令提示符处依次执行“net stop was /y”和“net start w3svc”，了解系统路径的更改）********。

## <a name="choose-a-deployment-option"></a>选择部署选项

如果您需要将应用部署到 IIS 的帮助，请考虑以下选项：

* 通过在 IIS 中创建发布设置文件并在 Visual Studio 中导入设置进行部署。 在某些情况下，这是部署应用的快速方法。 创建发布设置文件时，权限将自动在 IIS 中设置。

* 通过发布到本地文件夹，并通过首选方法将输出复制到 IIS 上准备好的应用文件夹进行部署。

## <a name="optional-deploy-using-a-publish-settings-file"></a>（可选）使用发布设置文件进行部署

您可以使用此选项创建发布设置文件并将其导入 Visual Studio。

> [!NOTE]
> 此部署方法使用 Web 部署。 如果要在 Visual Studio 中手动配置 Web 部署，而不是导入设置，则可以安装 Web 部署 3.6，而不是为托管服务器安装 Web 部署 3.6。 但是，如果手动配置 Web 部署，则需要确保服务器上的应用文件夹配置了正确的值和权限（请参阅[配置ASP.NET网站](#BKMK_deploy_asp_net)）。

### <a name="install-and-configure-web-deploy-for-hosting-servers-on-windows-server"></a>安装和配置 Web 部署，用于在 Windows 服务器上托管服务器

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/install-web-deploy-with-hosting-server.md)]

### <a name="create-the-publish-settings-file-in-iis-on-windows-server"></a>在 Windows Server 上的 IIS 中创建发布设置文件

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/create-publish-settings-iis.md)]

### <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>在 Visual Studio 中导入发布设置并进行部署

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/import-publish-settings-vs.md)]

应用成功部署后，它应自动启动。 如果应用不是从 Visual Studio 启动的，则在 IIS 中启动应用。 对于 ASP.NET Core，需要确保将 DefaultAppPool 的应用程序池字段设置为“无托管代码”********。

1. 在 **"设置"** 对话框中，通过单击 **"下一步**"来启用调试，选择 **"调试**"配置，然后在 **"文件发布**"选项下选择 **"删除目标的其他文件**"。

    > [!NOTE]
    > 如果选择"发布"配置，则在发布时禁用*Web.config*文件中的调试。

1. 单击 **"保存**"，然后重新发布应用。

## <a name="optional-deploy-by-publishing-to-a-local-folder"></a>（可选）通过发布到本地文件夹进行部署

如果要使用 PowerShell、RoboCopy 将应用复制到 IIS，或者想要手动复制文件，则可以使用此选项来部署应用。

### <a name="configure-the-aspnet-core-web-site-on-the-windows-server-computer"></a><a name="BKMK_deploy_asp_net"></a>在 Windows 服务器计算机上配置ASP.NET核心网站

如果要导入发布设置，可以跳过此部分。

1. 打开“Internet 信息服务(IIS)管理器” **** 并转到“站点” ****。

2. 右键单击“默认网站” **** 节点，然后选择“添加应用程序” ****。

3. 将**别名**字段设置为**MyASApp，** 将应用程序池字段设置为 **"无托管代码**"。 将**物理路径**设置为**C：\发布**（稍后将部署ASP.NET核心项目）。

4. 在 IIS 管理器中选择网站后，选择 **"编辑权限**"，并确保为应用程序池配置的 IUSR、IIS_IUSRS 或用户是具有读取&执行权限的授权用户。

    如果您没有看到这些用户之一具有访问权限，请执行步骤，将 IUSR 添加为具有读取&执行权限的用户。

### <a name="optional-publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>（可选）通过从可视化工作室发布到本地文件夹来发布和部署应用

如果不使用 Web 部署，则必须使用文件系统或其他工具发布和部署应用。 您可以首先使用文件系统创建包，然后手动部署包或使用其他工具（如 PowerShell、RoboCopy 或 XCopy）。 在本节中，我们假设您正在手动复制包，如果您不使用 Web 部署。

[!INCLUDE [remote-debugger-deploy-app-local](../debugger/includes/remote-debugger-deploy-app-local.md)]

### <a name="download-and-install-the-remote-tools-on-windows-server"></a><a name="BKMK_msvsmon"></a>在 Windows 服务器上下载并安装远程工具

下载与您的 Visual Studio 版本相匹配的远程工具版本。

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

### <a name="set-up-the-remote-debugger-on-windows-server"></a><a name="BKMK_setup"></a>在 Windows 服务器上设置远程调试器

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 如果需要为其他用户添加权限，请更改身份验证模式或远程调试器的端口号，请参阅[配置远程调试器](../debugger/remote-debugging.md#configure_msvsmon)。

### <a name="attach-to-the-aspnet-application-from-the-visual-studio-computer"></a><a name="BKMK_attach"></a> 从 Visual Studio 计算机附加到 ASP.NET 应用程序

1. 在 Visual Studio 计算机上，打开您尝试调试的解决方案（如果您正在按照本文中的步骤操作，则**MyASApp）。**
2. 在可视化工作室中，单击**调试>附加到进程**（Ctrl = Alt = P）。

    > [!TIP]
    > 在 Visual Studio 2017 和更高版本中，您可以使用**调试>重新附加到进程...**

3. 将"限定符"字段设置为**\<远程计算机名称>，** 然后按**Enter**。

    验证 Visual Studio 是否将所需的端口添加到计算机名称，该端口以格式显示：**\<远程计算机名称>：端口**

    ::: moniker range=">=vs-2019"
    在 Visual Studio 2019 上，您应该会看到**\<远程计算机名称>：4024**
    ::: moniker-end
    ::: moniker range="vs-2017"
    在 Visual Studio 2017 上，您应该会看到**\<远程计算机名称>：4022**
    ::: moniker-end
    端口是必需的。 如果看不到端口号，则手动添加它。

4. 单击“刷新”。****
    “可用进程” **** 窗口中将显示某些进程。

    如果看不到任何进程，请尝试使用 IP 地址而不是远程计算机名称（需要端口）。 您可以在`ipconfig`命令行中使用来获取 IPv4 地址。

    如果要使用 **"查找"** 按钮，可能需要在服务器上[打开 UDP 端口 3702。](#bkmk_openports)

5. 勾选“显示所有用户的进程”  ****。

6. 键入进程名称的第一个字母以快速查找应用。

    * 选择**dotnet.exe（** 对于 .NET 核心）

      如果有多个进程显示**dotnet.exe，** 请检查**用户名**列。 在某些情况下，"**用户名**"列显示应用池名称，例如**IIS APPPOOL_默认AppPool。** 如果看到应用池，识别正确过程的一种简单方法是为要调试的应用实例创建新的名为 App Pool，然后您可以在 **"用户名"** 列中轻松找到它。

    * 在某些 IIS 方案中，您可能会在进程列表中找到应用名称，例如**MyASPApp.exe**。 您可以附加到此过程。

    ::: moniker range=">=vs-2019"
    ![RemoteDBG_AttachToProcess](../debugger/media/vs-2019/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end

7. 单击 **"附加**"。

8. 打开远程计算机的网站。 在浏览器中，转到 http://\<remote computer name>****。

    将显示 ASP.NET 网页。
9. 在正在运行的ASP.NET应用程序中，单击指向 **"关于"** 页面的链接。

    应在 Visual Studio 中命中断点。

### <a name="troubleshooting-open-required-ports-on-windows-server"></a><a name="bkmk_openports"></a> 疑难解答Windows Server 上打开所需的端口

在大多数设置中，通过安装ASP.NET和远程调试器打开所需的端口。 但是，如果要解决部署问题，并且应用托管在防火墙后面，则可能需要验证正确的端口是否打开。

在 Azure VM 上，必须通过[网络安全组](/azure/virtual-machines/windows/nsg-quickstart-portal)打开端口。

所需端口：

* 80 - IIS 需要
::: moniker range=">=vs-2019"
* 4024 - 从 Visual Studio 2019 进行远程调试所需的（有关详细信息，请参阅[远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)）。
::: moniker-end
::: moniker range="vs-2017"
* 4022 - 从 Visual Studio 2017 进行远程调试所需的（有关详细信息，请参阅[远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)）。
::: moniker-end
* UDP 3702 - （可选） 发现端口使您能够在连接到 Visual Studio 中的远程调试器时使用 **"查找**"按钮。

此外，这些端口应该已经通过ASP.NET安装打开：
- 8172 - （可选）从可视化工作室部署应用所需的 Web 部署
