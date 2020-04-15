---
title: 远程 iIS 计算机上的远程调试ASP.NET核心 |微软文档
ms.custom: remotedebugging
ms.date: 05/21/2018
ms.topic: conceptual
ms.assetid: 573a3fc5-6901-41f1-bc87-557aa45d8858
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: b33ead969456935dab54c042ba4fbaf1f5ff44f4
ms.sourcegitcommit: cc58ca7ceae783b972ca25af69f17c9f92a29fc2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "81385482"
---
# <a name="remote-debug-aspnet-core-on-a-remote-iis-computer-in-visual-studio"></a>远程调试ASP.NET可视化演播室远程 IIS 计算机上的核心

要调试已部署到 IIS 的ASP.NET核心应用程序，请在部署应用的计算机上安装并运行远程工具，然后从 Visual Studio 附加到正在运行的应用。

![远程调试器组件](../debugger/media/remote-debugger-aspnet.png "Remote_debugger_components")

本指南介绍如何设置和配置 Visual Studio ASP.NET核心，将其部署到 IIS，以及从 Visual Studio 连接远程调试器。 要ASP.NET 4.5.2 远程调试，请参阅[IIS 计算机上的远程调试ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)。 您还可以使用 Azure 在 IIS 上部署和调试。 对于 Azure 应用服务，可以使用[快照调试器](../debugger/debug-live-azure-applications.md)或[从服务器资源管理器 附加调试器](../debugger/remote-debugging-azure.md)，轻松在预配置的 IIS 实例和远程调试器上部署和调试。

## <a name="prerequisites"></a>先决条件

::: moniker range=">=vs-2019"
Visual Studio 2019 需要遵循本文中所示的步骤。
::: moniker-end
::: moniker range="vs-2017"
Visual Studio 2017 需要遵循本文中所示的步骤。
::: moniker-end

这些过程已在以下服务器配置上过测试：
* Windows 服务器 2012 R2 和 IIS 8
* Windows 服务器 2016 和 IIS 10

## <a name="network-requirements"></a>网络要求

不支持在通过代理连接的两台计算机之间进行调试。 不建议通过高延迟或低带宽连接（如拨号 Internet）或跨国家/地区的 Internet 进行调试，并且可能会失败或速度过慢，令人无法接受。 有关需求的完整列表，请参阅[要求](../debugger/remote-debugging.md#requirements_msvsmon)。

## <a name="app-already-running-in-iis"></a>已在 IIS 中运行的应用？

本文包括有关在 Windows 服务器上设置 IIS 的基本配置和从 Visual Studio 部署应用的步骤。 包括这些步骤，以确保服务器已安装所需的组件，应用可以正常运行，并且您已准备好进行远程调试。

* 如果你的应用在 IIS 中运行，并且只想下载远程调试器并开始调试，请转到 Windows[服务器上下载并安装远程工具](#BKMK_msvsmon)。

* 如果希望帮助确保应用在 IIS 中设置、部署和正确运行，以便可以调试，请按照本主题中的所有步骤操作。

## <a name="create-the-aspnet-core-application-on-the-visual-studio-computer"></a>在可视化工作室计算机上创建ASP.NET核心应用程序

1. 创建新的 ASP.NET Core Web 应用呈现。 

    ::: moniker range=">=vs-2019"
    在 Visual Studio 2019 中，键入**Ctrl + Q**以打开搜索框，键入**asp.net，** 选择**模板**，然后选择**创建新ASP.NET核心 Web 应用程序**。 在显示的对话框中，为项目**MyASApp**命名 ，然后选择"**创建**"。 接下来，选择**Web 应用程序（模型视图控制器），** 然后选择 **"创建**"。
    ::: moniker-end
    ::: moniker range="vs-2017"
    在 Visual Studio 2017 中，选择 **"文件>新的>项目**，然后选择**Visual C# > Web >ASP.NET核心 Web 应用程序**。 在"ASP.NET核心模板部分中，选择**Web 应用程序（模型-视图控制器）**。 请确保选择了ASP.NET核心 2.1，未选择**启用 Docker 支持**，并且**身份验证**设置为 **"无身份验证**"。 命名项目**MyASApp**。
    ::: moniker-end

4. 打开About.cshtml.cs文件并在`OnGet`方法中设置断点（在较旧的模板中，改为打开HomeController.cs并在`About()`方法中设置断点）。

## <a name="install-and-configure-iis-on-windows-server"></a><a name="bkmk_configureIIS"></a>在 Windows 服务器上安装和配置 IIS

[!INCLUDE [remote-debugger-install-iis-role](../debugger/includes/remote-debugger-install-iis-role.md)]

## <a name="update-browser-security-settings-on-windows-server"></a>更新 Windows 服务器上的浏览器安全设置

如果在 Internet 资源管理器中启用了增强的安全配置（默认情况下已启用），则可能需要将某些域添加为受信任的站点，以便能够下载某些 Web 服务器组件。 通过访问**互联网选项>安全>受信任网站>网站**添加受信任的网站。 添加以下域。

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

下载软件时，您可能会收到请求，请求授予加载各种网站脚本和资源的权限。 其中一些资源不是必需的，但为了简化该过程，请在提示时单击 **"添加**"。

## <a name="install-aspnet-core-on-windows-server"></a>在 Windows 服务器上安装 ASP.NET 核心

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

1. 打开 Windows 资源管理器并创建新文件夹**C：\Publish，** 稍后将部署ASP.NET核心项目。

2. 如果尚未打开，则打开**互联网信息服务 （IIS） 管理器**。 （在服务器管理器的左侧窗格中，选择**IIS**。 右键单击服务器并选择“Internet Information Services (IIS)管理器”****。）

3. 在左侧窗格中的 **"连接"** 下，转到 **"网站**"。

4. 选择**默认网站**，选择 **"基本设置**"，并将**物理路径**设置为**C：\发布**。

4. 右键单击“默认网站” **** 节点，然后选择“添加应用程序” ****。

5. 将**别名**字段设置为**MyASApp，** 接受默认应用程序池 （**默认AppPool），** 并将**物理路径**设置为**C：\发布**。

6. 在 **"连接"** 下，选择**应用程序池**。 打开**默认应用程序池**并将应用程序池字段设置为 **"无托管代码**"。

7. 右键单击 IIS 管理器中的新网站，选择 **"编辑权限**"，并确保 IUSR、IIS_IUSRS 或配置为访问 Web 应用的用户是具有读取&执行权限的授权用户。

    如果您没有看到这些用户之一具有访问权限，请执行步骤，将 IUSR 添加为具有读取&执行权限的用户。

### <a name="publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>通过从可视化工作室发布到本地文件夹来发布和部署应用

您还可以使用文件系统或其他工具发布和部署应用。

[!INCLUDE [remote-debugger-deploy-app-local](../debugger/includes/remote-debugger-deploy-app-local.md)]

## <a name="download-and-install-the-remote-tools-on-windows-server"></a><a name="BKMK_msvsmon"></a>在 Windows 服务器上下载并安装远程工具

下载与您的 Visual Studio 版本相匹配的远程工具版本。

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

## <a name="set-up-the-remote-debugger-on-windows-server"></a><a name="BKMK_setup"></a>在 Windows 服务器上设置远程调试器

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 如果需要为其他用户添加权限，请更改身份验证模式或远程调试器的端口号，请参阅[配置远程调试器](../debugger/remote-debugging.md#configure_msvsmon)。

有关将远程调试器作为服务运行的信息，请参阅[将远程调试器作为服务运行](../debugger/remote-debugging.md#bkmk_configureService)。

## <a name="attach-to-the-aspnet-application-from-the-visual-studio-computer"></a><a name="BKMK_attach"></a> 从 Visual Studio 计算机附加到 ASP.NET 应用程序

1. 在 Visual Studio 计算机上，打开您尝试调试的解决方案（如果您正在按照本文中的所有步骤操作**MyASApp）。**
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

    * 如果您正在 IIS 上使用[应用内托管模型](/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-3.1#hosting-models)，请选择正确的**w3wp.exe**进程。 从 .NET 核心 3 开始，这是默认值。

    * 否则，选择**dotnet.exe**进程。 （这是进程外托管模型。

    如果有多个进程显示*w3wp.exe*或*dotnet.exe，* 请检查**用户名**列。 在某些情况下，"**用户名**"列显示应用池名称，例如**IIS APPPOOL_默认AppPool。** 如果看到应用池，但它不唯一，请为要调试的应用实例创建新的名为 App Pool，然后您可以在 **"用户名"** 列中轻松找到它。

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

## <a name="troubleshooting-open-required-ports-on-windows-server"></a><a name="bkmk_openports"></a> 疑难解答Windows Server 上打开所需的端口

在大多数设置中，通过安装ASP.NET和远程调试器打开所需的端口。 但是，您可能需要验证端口是否处于打开状态。

> [!NOTE]
> 在 Azure VM 上，必须通过[网络安全组](/azure/virtual-machines/windows/nsg-quickstart-portal)打开端口。

所需端口：

* 80 - IIS 需要
::: moniker range=">=vs-2019"
* 4024 - 从 Visual Studio 2019 进行远程调试所需的（有关详细信息，请参阅[远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)）。
::: moniker-end
::: moniker range="vs-2017"
* 4022 - 从 Visual Studio 2017 进行远程调试所需的（有关详细信息，请参阅[远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)）。
::: moniker-end
* UDP 3702 - （可选） 发现端口使您能够在连接到 Visual Studio 中的远程调试器时使用 **"查找**"按钮。

1. 要打开 Windows 服务器上的端口，打开 **"开始"** 菜单，搜索**具有高级安全性**的 Windows 防火墙 。

2. 然后选择 **"入站规则>>端口的新规则**，然后单击"**下一步**"。 （对于 UDP 3702，请选择**出站规则**。

3. 在 **"特定本地端口**"下，输入端口号，单击 **"下一步**"。

4. 单击"**允许连接**"，单击 **"下一步**"。

5. 选择要启用端口的一个或多个网络类型，然后单击"**下一步**"。

    你选择的类型必须包括远程计算机连接到的网络。
6. 为入站规则添加名称（例如 **，IIS、Web****部署**或**msvsmon），** 然后单击 **"完成**"。

    应该能在“入站规则”或“出站规则”列表中看到自己的新规则。

    如果需要有关配置 Windows 防火墙的更多详细信息，请参阅[为远程调试配置 Windows 防火墙](../debugger/configure-the-windows-firewall-for-remote-debugging.md)。

3. 为其他必需的端口创建其他规则。
