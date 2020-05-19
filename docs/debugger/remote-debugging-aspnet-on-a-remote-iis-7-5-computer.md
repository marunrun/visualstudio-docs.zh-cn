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
ms.openlocfilehash: 86b035164c4d34f4ce0182ea51fdfe6381ad2d4f
ms.sourcegitcommit: 08c144d290da373df841f04fc799e3133540a541
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2019
ms.locfileid: "72536019"
---
# <a name="remote-debug-aspnet-on-a-remote-iis-computer"></a>远程调试远程 IIS 计算机上的 ASP.NET
若要调试已部署到 IIS 的 ASP.NET 应用程序，请在部署了应用的计算机上安装并运行远程工具，然后从 Visual Studio 附加到正在运行的应用。

![远程调试器组件](../debugger/media/remote-debugger-aspnet.png "Remote_debugger_components")

本指南说明如何设置和配置 Visual Studio ASP.NET MVC 4.5.2 应用程序，将其部署到 IIS，并从 Visual Studio 附加远程调试器。

> [!NOTE]
> 若要改为远程调试 ASP.NET Core，请参阅[远程调试 IIS 计算机上的 ASP.NET Core](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)。 对于 Azure 应用服务，可以使用 [Snapshot Debugger](../debugger/debug-live-azure-applications.md)（需要 .NET 4.6.1）或通过[从服务器资源管理器附加调试器](../debugger/remote-debugging-azure.md)，在预先配置的 IIS 实例上轻松部署和调试。

## <a name="prerequisites"></a>先决条件

::: moniker range=">=vs-2019"
需要安装 Visual Studio 2019 才能执行本文所述的步骤。
::: moniker-end
::: moniker range="vs-2017"
需要安装 Visual Studio 2017 才能执行本文所述的步骤。
::: moniker-end

这些过程已在以下服务器配置上进行了测试：
* Windows Server 2012 R2 和 IIS 8（对于 Windows Server 2008 R2，服务器步骤有所不同）

## <a name="network-requirements"></a>网络要求

从 Windows Server 2008 Service Pack 2 开始，Windows Server 支持远程调试器。 有关要求的完整列表，请参阅[要求](../debugger/remote-debugging.md#requirements_msvsmon)。

> [!NOTE]
> 不支持在通过代理连接的两台计算机之间进行调试。 不建议通过高延迟或低带宽连接（例如拨号 Internet）或在跨国家/地区的 Internet 上进行调试，否则可能会导致调试失败或速度过慢。

## <a name="app-already-running-in-iis"></a>应用已在 IIS 中运行？

本文包含有关在 Windows Server 上设置 IIS 的基本配置以及从 Visual Studio 部署应用的步骤。 这些步骤可确保服务器安装了必需的组件，应用可以正常运行，以及你已经准备好进行远程调试。

* 如果应用正在 IIS 中运行，你只想下载远程调试器并启动调试，请转到[在 Windows Server 上下载并安装远程工具](#BKMK_msvsmon)。

* 如果需要帮助确保在 IIS 中正确设置、部署和运行应用，以便进行调试，请按照本主题中的所有步骤进行操作。

## <a name="create-the-aspnet-452-application-on-the-visual-studio-computer"></a>在 Visual Studio 计算机上创建 ASP.NET 4.5.2 应用程序

1. 创建新的 MVC ASP.NET 应用程序。

    ::: moniker range=">=vs-2019"
    在 Visual Studio 2019 中，键入 Ctrl+Q 打开搜索框，键入“asp.net”，选择“模板”，然后选择“创建新的 ASP.NET Web 应用程序(.NET Framework)”   。 在出现的对话框中，将项目命名为“MyASPApp”，然后选择“创建” 。 选择“MVC”，并选择“创建” 。
    ::: moniker-end
    ::: moniker range="vs-2017"
    若要在 Visual Studio 2017 中执行此操作，请选择“文件”>“新建”>“项目”，然后选择“Visual C#”>“Web”>“ASP.NET Web 应用程序”。 在 **ASP.NET 4.5.2** 模板部分中，选择“MVC” 。 请确保未选择“启用 Docker 支持”，并且“身份验证”设置为“无身份验证”。 将项目命名为 MyASPApp。）
    ::: moniker-end

2. 打开 HomeController.cs 文件，并在 `About()` 方法中设置断点。

## <a name="install-and-configure-iis-on-windows-server"></a><a name="bkmk_configureIIS"></a> 在 Windows Server 上安装和配置 IIS

[!INCLUDE [remote-debugger-install-iis-role](../debugger/includes/remote-debugger-install-iis-role.md)]

## <a name="update-browser-security-settings-on-windows-server"></a>更新 Windows Server 上的浏览器安全设置

如果在 Internet Explorer 中启用了“增强的安全配置”（默认情况下已启用），则可能需要将某些域添加为受信任的站点，以便下载某些 Web 服务器组件。 通过转到“Internet 选项”>“安全性”>“受信任的站点”>“站点”来添加受信任的站点。 添加以下域。

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

下载软件时，可能会收到授权加载各种网站脚本和资源的请求。 其中一些资源不是必需的，但为了简化此过程，请在出现提示时单击“添加”。

## <a name="install-aspnet-45-on-windows-server"></a><a name="BKMK_deploy_asp_net"></a> 在 Windows Server 上安装 ASP.NET 4.5

如果需要在 IIS 上安装 ASP.NET 的详细信息，请参阅[使用 ASP.NET 3.5 和 ASP.NET 4.5 的 IIS 8.0](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)。

1. 在服务器管理器的左窗格中，选择“IIS”。 右键单击服务器并选择“Internet Information Services (IIS)管理器”。

1. 使用 Web 平台安装程序 (WebPI) 安装 ASP.NET 4.5（从 Windows Server 2012 R2 的服务器节点，选择“获取新 Web 平台组件”，然后搜索 ASP.NET）

    ![RemoteDBG_IIS_AspNet_45](../debugger/media/remotedbg_iis_aspnet_45.png "RemoteDBG_IIS_AspNet_45")

    > [!NOTE]
    > 如果使用 Windows Server 2008 R2，请改为使用以下命令安装 ASP.NET 4：

     **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -ir**

2. 重启系统（或在命令提示符处依次执行“net stop was /y”和“net start w3svc”，了解系统路径的更改） 。

## <a name="choose-a-deployment-option"></a>选择部署选项

如果需要帮助将应用部署到 IIS，请考虑以下选项：

* 通过在 IIS 中创建发布设置文件并在 Visual Studio 中导入设置来进行部署。 在某些情况下，这是一种快速部署应用的方法。 当你创建发布设置文件时，系统会在 IIS 中自动设置权限。

* 通过发布到本地文件夹并使用首选方法将输出复制到 IIS 上准备就绪的应用文件夹来进行部署。

## <a name="optional-deploy-using-a-publish-settings-file"></a>（可选）使用发布设置文件进行部署

可以使用此选项创建一个发布设置文件，并将其导入到 Visual Studio 中。

> [!NOTE]
> 此部署方法使用 Web 部署。 如果要在 Visual Studio 中手动配置 Web 部署，而不是导入设置，则可以安装 Web 部署 3.6，而不是用于宿主服务器的 Web 部署 3.6。 但是，如果手动配置 Web 部署，则需要确保使用正确的值和权限配置服务器上的应用文件夹（请参阅[配置 ASP.NET 网站](#BKMK_deploy_asp_net)）。

### <a name="install-and-configure-web-deploy-for-hosting-servers-on-windows-server"></a>在 Windows Server 上安装和配置用于宿主服务器的 Web 部署

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/install-web-deploy-with-hosting-server.md)]

### <a name="create-the-publish-settings-file-in-iis-on-windows-server"></a>在 Windows Server 上的 IIS 中创建发布设置文件

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/create-publish-settings-iis.md)]

### <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>在 Visual Studio 中导入发布设置并进行部署

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/import-publish-settings-vs.md)]

应用成功部署后，它应自动启动。 如果在 Visual Studio 中无法启动应用，请在 IIS 中启动。

1. 在“设置”对话框中，单击“下一步”启用调试，选择“调试”配置，然后在“文件发布”选项下选择“删除目标处的其他文件”。

    > [!NOTE]
    > 如果选择发布配置，则在发布时，需要在 web.config 文件中禁用调试。

1. 单击“保存”，然后重新发布应用。

## <a name="optional-deploy-by-publishing-to-a-local-folder"></a>（可选）通过发布到本地文件夹进行部署

如果要使用 PowerShell、RoboCopy 将应用复制到 IIS，或者要手动复制文件，则可以使用此选项来部署应用。

### <a name="configure-the-aspnet-web-site-on-the-windows-server-computer"></a><a name="BKMK_deploy_asp_net"></a> 在 Windows Server 计算机上配置 ASP.NET 网站

1. 打开 Windows 资源管理器并创建新文件夹 C:\Publish，以后将在其中部署 ASP.NET 项目。

2. 如果尚未打开，请打开“Internet Information Services (IIS) 管理器”。 （在服务器管理器的左窗格中，选择“IIS”。 右键单击服务器并选择“Internet Information Services (IIS)管理器”。）

3. 在左窗格中的“连接”下，转到“站点”。

4. 选择“默认网站”，选择“基本设置”，然后将“物理路径”设置为“C:\Publish”。

5. 右键单击“默认网站”  节点，然后选择“添加应用程序” 。

6. 将“别名”字段设置为“MyASPApp”，接受默认应用程序池 (DefaultAppPool)，并将“物理路径”设置“C:\Publish”。

7. 在“连接”下，选择“应用程序池”。 打开 DefaultAppPool 并将“应用程序池”字段设置为“ASP.NET v4.0”（ASP.NET 4.5 不是应用程序池的选项）。

8. 在 IIS 管理器中选择了站点后，选择“编辑权限”，并确保为应用程序池配置的 IUSR、IIS_IUSRS 或用户是拥有读取和执行权限的授权用户。 如果这些用户都不存在，请将 IUSR 添加为拥有读取和执行权限的用户。

### <a name="publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>通过从 Visual Studio 发布到本地文件夹来发布和部署应用

还可以使用文件系统或其他工具发布和部署应用。

1. (ASP.NET 4.5.2) 确保 web.config 文件列出了 .NET 的正确版本。  例如，如果面向 ASP.NET 4.5.2，请确保此版本在 web.config 中列出。

    ```xml
    <system.web>
      <compilation debug="true" targetFramework="4.5.2" />
      <httpRuntime targetFramework="4.5.2" />
      <httpModules>
        <add name="ApplicationInsightsWebTracking" type="Microsoft.ApplicationInsights.Web.ApplicationInsightsHttpModule, Microsoft.AI.Web" />
      </httpModules>
    </system.web>

    ```

    例如，如果安装 ASP.NET 4 而不是 4.5.2，则版本应为 4.0。

[!INCLUDE [remote-debugger-deploy-app-local](../debugger/includes/remote-debugger-deploy-app-local.md)]

## <a name="download-and-install-the-remote-tools-on-windows-server"></a><a name="BKMK_msvsmon"></a> 在 Windows Server 上下载并安装远程工具

下载与 Visual Studio 版本匹配的远程工具版本。

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

## <a name="set-up-the-remote-debugger-on-windows-server"></a><a name="BKMK_setup"></a> 在 Windows Server 上设置远程调试器

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 如果需要为其他用户添加权限，请更改远程调试器的身份验证模式或端口号，请参阅[配置远程调试器](../debugger/remote-debugging.md#configure_msvsmon)。

有关将远程调试器作为服务运行的信息，请参阅[将远程调试器作为服务运行](../debugger/remote-debugging.md#bkmk_configureService)。

## <a name="attach-to-the-aspnet-application-from-the-visual-studio-computer"></a><a name="BKMK_attach"></a> 从 Visual Studio 计算机附加到 ASP.NET 应用程序

1. 在 Visual Studio 计算机上，打开尝试调试的解决方案（如果按照本文中的步骤操作，则是 MyASPApp）。
2. 在 Visual Studio 中，单击“调试”>“附加到进程”(Ctrl + Alt + P)。

    > [!TIP]
    > 在 Visual Studio 2017 及更高版本中，可以使用“调试”>“重新附加到进程...”重新附加到以前附加到的同一进程(Shift+Alt+P)。

3. 将限定符字段设置为“\<remote computer name>”并按 Enter 。

    确保 Visual Studio 将所需的端口添加到计算机名称中，其格式为：\<remote computer name>:port

    ::: moniker range=">=vs-2019"
    在 Visual Studio 2019 上，应看到 \<remote computer name>:4024
    ::: moniker-end
    ::: moniker range="vs-2017"
    在 Visual Studio 2017 上，应看到 \<remote computer name>:4022
    ::: moniker-end
    端口是必需的。 如果看不到端口号，请手动添加。

4. 单击“刷新”。
    “可用进程”  窗口中将显示某些进程。

    如果看不到任何进程，请尝试使用 IP 地址而不是远程计算机名称（端口是必需的）。 可以在命令行中使用 `ipconfig` 来获取 IPv4 地址。

5. 勾选“显示所有用户的进程”  。

6. 键入进程名称的第一个字母，以快速查找 w3wp.exe（适用于 ASP.NET 4.5）。

    如果有多个显示 w3wp.exe 的进程，请检查“用户名”列。 在某些情况下，“用户名”列显示应用池名称，例如 IIS APPPOOL\DefaultAppPool 。 如果你看到应用池，则一种确定正确进程的简单方法是为要调试的应用实例创建新的命名应用池，随后可以在“用户名”列中轻松找到它。

    ::: moniker range=">=vs-2019"
    ![RemoteDBG_AttachToProcess](../debugger/media/vs-2019/remotedbg-attachtoprocess.png "RemoteDBG_AttachToProcess")
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg-attachtoprocess.png "RemoteDBG_AttachToProcess")
    ::: moniker-end

7. 单击“附加”

8. 打开远程计算机的网站。 在浏览器中，转到 http://\<remote computer name>。

    将显示 ASP.NET 网页。
9. 在正在运行的 ASP.NET 应用程序中，单击指向“关于”页面的链接。

    应在 Visual Studio 中命中断点。

## <a name="troubleshooting-open-required-ports-on-windows-server"></a><a name="bkmk_openports"></a> 排除故障：在 Windows Server 上打开必需端口

在大多数设置中，必需端口通过安装 ASP.NET 和远程调试器来打开。 但是，你可能需要验证端口是否已打开。

> [!NOTE]
> 在 Azure VM 上，必须通过[网络安全组](/azure/virtual-machines/windows/nsg-quickstart-portal)打开端口。

必需端口：

* 80 - 对于 IIS 是必需的
::: moniker range=">=vs-2019"
* 4024 - 从 Visual Studio 2019 进行远程调试时必需（有关详细信息，请参阅[远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)）。
::: moniker-end
::: moniker range="vs-2017"
* 4022 - 从 Visual Studio 2017 进行远程调试时必需（有关详细信息，请参阅[远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)）。
::: moniker-end
* UDP 3702 -（可选）发现端口允许你在附加到 Visual Studio 中的远程调试器时使用“查找”按钮。

1. 若要在 Windows Server 上打开端口，请打开“开始”菜单，搜索“高级安全 Windows 防火墙”。

2. 然后选择“入站规则”>“新建规则”>“端口”。 选择“下一步”，在“特定本地端口”下，输入端口号，单击“下一步”，然后单击“允许连接”，单击“下一步”，然后为入站规则添加名称（“IIS”、“Web 部署”或“msvsmon”）。

    如果需要有关配置 Windows 防火墙的详细信息，请参阅[配置 Windows 防火墙以便进行远程调试](../debugger/configure-the-windows-firewall-for-remote-debugging.md)。

3. 为其他必需端口创建附加规则。