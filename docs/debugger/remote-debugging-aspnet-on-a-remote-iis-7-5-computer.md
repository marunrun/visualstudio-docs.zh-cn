---
title: 远程调试 IIS 计算机上的 ASP.NET
ms.custom:
- remotedebugging
- seodec18
ms.date: 05/21/2018
ms.topic: conceptual
ms.assetid: 9cb339b5-3caf-4755-aad1-4a5da54b2a23
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: ba255d1d1e906e8fe7bacd05d1f4afd4b7bf413b
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63407845"
---
# <a name="remote-debug-aspnet-on-a-remote-iis-computer"></a>远程调试远程 IIS 计算机上的 ASP.NET
若要调试已部署到 IIS 的 ASP.NET 应用程序，安装和运行远程工具的计算机上在其中部署您的应用程序，然后从 Visual Studio 附加到正在运行的应用。

![远程调试器组件](../debugger/media/remote-debugger-aspnet.png "Remote_debugger_components")

本指南介绍如何设置和配置 Visual Studio ASP.NET MVC 4.5.2 应用程序、 将其部署到 IIS，并从 Visual Studio 附加远程调试器。

> [!NOTE]
> 远程调试 ASP.NET Core，而是，请参阅[IIS 计算机上的远程调试 ASP.NET Core](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)。 可以轻松地部署和调试 IIS 使用的预配置实例上的 Azure 应用服务[快照调试器](../debugger/debug-live-azure-applications.md)(.NET 4.6.1 所需) 或通过[将调试器附加服务器资源管理器](../debugger/remote-debugging-azure.md)。

## <a name="prerequisites"></a>系统必备

::: moniker range=">=vs-2019"
Visual Studio 2019 需按照本文中所示的步骤。
::: moniker-end
::: moniker range="vs-2017"
Visual Studio 2017 需要按照本文中所示的步骤。
::: moniker-end

这些服务器配置上进行了测试这些过程：
* Windows Server 2012 R2 和 IIS 8 （对于 Windows Server 2008 R2 中，服务器，步骤会有所不同）

## <a name="network-requirements"></a>网络要求

从 Windows Server 2008 Service Pack 2 的 Windows Server 支持远程调试器。 有关要求的完整列表，请参阅[要求](../debugger/remote-debugging.md#requirements_msvsmon)。

> [!NOTE]
> 不支持调试通过代理连接的两台计算机之间。 调试通过高延迟或低带宽连接，例如拨号 Internet，或通过 Internet 跨国家/地区不建议并可能会失败或很令人无法接受慢。

## <a name="app-already-running-in-iis"></a>已在 IIS 中运行应用程序吗？

本文包含有关 Windows server 上的 IIS 的基本配置设置和部署该应用程序从 Visual Studio 的步骤。 这些步骤是包括在内，以确保服务器具有必需的安装，可以正确，运行该应用程序，您就为远程调试组件。

* 如果在 IIS 中运行您的应用程序，并且只是想要下载远程调试器和启动调试，请转到[下载并安装 Windows Server 上的远程工具](#BKMK_msvsmon)。

* 如果需要帮助，确保您的应用程序设置已完成，部署，并正确运行在 IIS 中，以便可以调试，请按照本主题中的所有步骤。

## <a name="create-the-aspnet-452-application-on-the-visual-studio-computer"></a>创建 ASP.NET 4.5.2 在 Visual Studio 计算机上应用程序

1. 创建新的 MVC ASP.NET 应用程序。

    ::: moniker range=">=vs-2019"
    在 Visual Studio 2019，键入**Ctrl + Q**若要打开搜索框中，键入**asp.net**，选择**模板**，然后选择**创建新 ASP.NET Web 应用程序 (.NET框架）** 。 在显示对话框中，该项目命名**MyASPApp**，然后选择**创建**。 选择**MVC** ，然后选择**创建**。
    ::: moniker-end
    ::: moniker range="vs-2017"
    若要执行此操作在 Visual Studio 2017 中，选择**文件 > 新建 > 项目**，然后选择**Visual C# > Web > ASP.NET Web 应用程序**。 在 **ASP.NET 4.5.2** 模板部分中，选择“MVC”  。 请确保**启用 Docker 支持**未选中并且**身份验证**设置为**无身份验证**。 将项目命名**MyASPApp**。)
    ::: moniker-end

2. 打开 HomeController.cs 文件，并在 `About()` 方法中设置断点。

## <a name="bkmk_configureIIS"></a> 安装和 Windows Server 上配置 IIS

[!INCLUDE [remote-debugger-install-iis-role](../debugger/includes/remote-debugger-install-iis-role.md)]

## <a name="update-browser-security-settings-on-windows-server"></a>更新 Windows Server 上的浏览器安全设置

如果在 Internet Explorer （默认情况下已启用） 中启用了增强的安全配置，您可能需要将某些域添加为受信任的站点，以便可以下载某些 web 服务器组件。 添加可信的站点，通过转到**Internet 选项 > 安全性 > 受信任的站点 > 站点**。 添加以下域。

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

下载软件时，可能会显示请求授予权限以加载各种 web 站点脚本和资源。 以下一些资源不是必需的但若要简化此过程中，单击**添加**出现提示时。

## <a name="BKMK_deploy_asp_net"></a> Windows Server 上安装 ASP.NET 4.5

如果你想要在 IIS 上安装 ASP.NET 的更多详细的信息，请参阅[IIS 8.0 使用 ASP.NET 3.5 和 ASP.NET 4.5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)。

1. 在服务器管理器的左窗格中，选择**IIS**。 右键单击服务器并选择“Internet Information Services (IIS)管理器”  。

1. 使用 Web 平台安装程序 (WebPI) 安装 ASP.NET 4.5 (从 Windows Server 2012 R2 中的服务器节点，选择**获取新的 Web 平台组件**，然后搜索 ASP.NET)

    ![RemoteDBG_IIS_AspNet_45](../debugger/media/remotedbg_iis_aspnet_45.png "RemoteDBG_IIS_AspNet_45")

    > [!NOTE]
    > 如果使用 Windows Server 2008 R2，安装 ASP.NET 4 改为使用此命令：

     **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -ir**

2. 重启系统（或在命令提示符处依次执行“net stop was /y”和“net start w3svc”，了解系统路径的更改）   。

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

应用成功部署后，它应自动启动。 如果从 Visual Studio 不启动应用程序，请在 IIS 中启动应用程序。

1. 在中**设置**对话框中，通过单击调试启用**下一步**，选择**调试**配置，然后选择**删除其他文件目标**下**文件发布**选项。

    > [!NOTE]
    > 如果选择发布配置，则禁用在中进行调试*web.config*文件在发布时。

1. 单击**保存**然后重新发布应用程序。

## <a name="optional-deploy-by-publishing-to-a-local-folder"></a>（可选）部署发布到本地文件夹

此选项可用于部署您的应用程序，如果你想要将应用程序复制到 IIS，使用 Powershell，RoboCopy，或者想要手动复制文件。

### <a name="BKMK_deploy_asp_net"></a> Windows Server 计算机上配置 ASP.NET 网站

1. 打开 Windows 资源管理器，并创建一个新文件夹**C:\Publish**、 更高版本将部署的 ASP.NET 项目。

2. 如果尚未打开，打开**Internet 信息服务 (IIS) 管理器**。 (在服务器管理器的左窗格中，选择**IIS**。 右键单击服务器并选择“Internet Information Services (IIS)管理器”  。）

3. 下**连接**在左窗格中，转到**站点**。

4. 选择**Default Web Site**，选择**基本设置**，并设置**物理路径**到**C:\Publish**。

5. 右键单击“默认网站”  节点，然后选择“添加应用程序”  。

6. 设置**别名**字段**MyASPApp**，接受默认应用程序池 (**DefaultAppPool**)，并设置**物理路径**到**C:\Publish**。

7. 下**连接**，选择**应用程序池**。 打开**DefaultAppPool**并将应用程序池字段设置为**ASP.NET v4.0** （ASP.NET 4.5 不是应用程序池的选项）。

8. 在 IIS 管理器中选择站点后，选择**编辑权限**，并确保该 IUSR、 IIS_IUSRS 或配置应用程序池为授权的用户使用读取和执行权限的用户。 如果没有任何这些用户不存在，将 IUSR 添加为具有读取和执行权限的用户。

### <a name="publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>发布和部署应用程序通过发布到本地文件夹从 Visual Studio

您还可以发布和部署应用程序使用文件系统或其他工具。

1. (ASP.NET 4.5.2)请确保 web.config 文件列出了.NET Framework 的正确版本。  例如，如果你面向的 ASP.NET 4.5.2，请确保在 web.config 中列出此版本。

    ```xml
    <system.web>
      <compilation debug="true" targetFramework="4.5.2" />
      <httpRuntime targetFramework="4.5.2" />
      <httpModules>
        <add name="ApplicationInsightsWebTracking" type="Microsoft.ApplicationInsights.Web.ApplicationInsightsHttpModule, Microsoft.AI.Web" />
      </httpModules>
    </system.web>

    ```

    例如，版本应为 4.0，如果您安装 ASP.NET 4，而不是 4.5.2。

[!INCLUDE [remote-debugger-deploy-app-local](../debugger/includes/remote-debugger-deploy-app-local.md)]

## <a name="BKMK_msvsmon"></a> 下载并安装 Windows Server 上的远程工具

下载与你的 Visual Studio 版本匹配远程工具的版本。

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

## <a name="BKMK_setup"></a> 设置 Windows Server 上的远程调试器

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 如果您需要添加其他用户的权限更改身份验证模式，或者远程调试器的端口号，请参阅[配置远程调试器](../debugger/remote-debugging.md#configure_msvsmon)。

有关运行远程调试器作为服务的信息，请参阅[远程调试器作为服务运行](../debugger/remote-debugging.md#bkmk_configureService)。

## <a name="BKMK_attach"></a> 从 Visual Studio 计算机附加到 ASP.NET 应用程序

1. Visual Studio 计算机上，打开要调试的解决方案 (**MyASPApp**在您按照这篇文章中的步骤)。
2. 在 Visual Studio 中，单击**调试 > 附加到进程**（Ctrl + Alt + P）。

    > [!TIP]
    > 在 Visual Studio 2017 和更高版本中，您可以重新附加到您以前使用附加到的同一个进程**调试 > 重新附加到进程...** (Shift + Alt + P)。

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

5. 勾选“显示所有用户的进程”   。

6. 键入进程名称，可以快速找到的第一个字母**w3wp.exe**为 ASP.NET 4.5。

    如果有多个进程显示**w3wp.exe**，检查**用户名**列。 在某些情况下，**用户名**列显示你的应用程序池名称，如**IIS APPPOOL\DefaultAppPool**。 如果你看到应用程序池标识正确的进程的简单办法是创建一个新应用池命名为你想要调试的应用程序实例，然后您可以找到它轻松地在**用户名**列。

    ::: moniker range=">=vs-2019"
    ![RemoteDBG_AttachToProcess](../debugger/media/vs-2019/remotedbg-attachtoprocess.png "RemoteDBG_AttachToProcess")
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg-attachtoprocess.png "RemoteDBG_AttachToProcess")
    ::: moniker-end

7. 单击“附加” 

8. 打开远程计算机的网站。 在浏览器中，转到 http://\<remote computer name>  。

    将显示 ASP.NET 网页。
9. 在运行的 ASP.NET 应用程序，单击链接到**有关**页。

    应在 Visual Studio 中命中断点。

## <a name="bkmk_openports"></a> 故障排除：Windows Server 上打开所需的端口

在大多数系统中，所需的端口被打开的 ASP.NET 和远程调试器安装。 但是，您可能需要验证端口打开。

> [!NOTE]
> 在 Azure VM 上，则必须打开端口通过[网络安全组](/azure/virtual-machines/windows/nsg-quickstart-portal)。

所需的端口：

* 80-所需的 IIS
::: moniker range=">=vs-2019"
* 4024-所需的 Visual Studio 2019 从远程调试 (请参阅[Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)有关详细信息)。
::: moniker-end
::: moniker range="vs-2017"
* 4022 的所需的从 Visual Studio 2017 远程调试 (请参阅[Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)有关详细信息)。
::: moniker-end
* UDP 3702-（可选） 发现端口使你能够**查找**按钮时将附加到 Visual Studio 中的远程调试器。

1. 若要打开 Windows 服务器上的端口，请打开**启动**菜单中，搜索**高级安全 Windows 防火墙**。

2. 然后选择**入站规则 > 新规则 > 端口**。 选择**下一步**并在**特定本地端口**，输入端口号，单击**下一步**，然后**允许连接**，单击下一步，和添加名称 (**IIS**， **Web Deploy**，或**msvsmon**) 的入站规则。

    如果您想配置 Windows 防火墙的详细信息，请参阅[配置 Windows 防火墙以进行远程调试](../debugger/configure-the-windows-firewall-for-remote-debugging.md)。

3. 创建其他规则中的其他所需的端口。