---
title: 远程调试 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.remote.overview
dev_langs:
- C++
- CSharp
- FSharp
- JScript
- VB
helpviewer_keywords:
- remote debugging, setup
ms.assetid: 5a94ad64-100d-43ca-9779-16cb5af86f97
caps.latest.revision: 81
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 68ebd9ab8c4f9d3cda1371d90a8da459edb1592b
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300568"
---
# <a name="remote-debugging"></a>远程调试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以调试已部署在另一台计算机的 Visual Studio 应用程序。  要进行此操作，可使用 Visual Studio 远程调试器。  
  
 此处的信息适用于 Windows 桌面应用程序和 ASP.NET 应用程序。  有关远程调试 Windows 应用商店应用程序和 Azure 应用程序的信息，请参阅[windows 应用商店和 azure 应用上的远程调试](#bkmk_winstoreAzure)。  
  
## <a name="get-the-remote-tools"></a>获取远程工具  
您可以直接在要调试的设备或服务器上下载远程工具，也可以从安装了 Visual Studio 的主机获取远程工具。

### <a name="to-download-and-install-the-remote-tools"></a>下载和安装远程工具
  
1. 在要调试的设备或服务器计算机（而不是运行 Visual Studio 的计算机）上，获取正确的远程工具版本。

    |版本|链接|注意|
    |-|-|-|
    |Visual Studio 2015 Update 3|[远程工具](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|如果系统提示，请加入免费的 Visual Studio Dev Essentials 组，或者只需使用有效的 Visual Studio 订阅进行登录。 然后，如有必要，请重新打开该链接。 始终下载与设备操作系统匹配的版本（x86、x64 或 ARM 版本）|
    |Visual Studio 2015 （较旧）|[远程工具](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|如果系统提示，请加入免费的 Visual Studio Dev Essentials 组，或者只需使用有效的 Visual Studio 订阅进行登录。 然后，如有必要，请重新打开该链接。|
    |Visual Studio 2013|[远程工具](https://msdn.microsoft.com/library/bt727f1t(v=vs.120).aspx#BKMK_Installing_the_Remote_Tools)|Visual Studio 2013 文档中的下载页面|
    |Visual Studio 2012|[远程工具](https://msdn.microsoft.com/library/bt727f1t(v=vs.110).aspx#BKMK_Installing_the_Remote_Tools)|Visual Studio 2012 文档中的下载页面|
  
2. 在 "下载" 页上，选择与你的操作系统（x86、x64 或 ARM 版本）匹配的工具版本，然后下载远程工具。
  
    > [!IMPORTANT]
    > 建议安装与 Visual Studio 版本匹配的最新版本的远程工具。 不推荐使用不匹配的版本。  
    >   
    >  此外，你必须安装与你要在其上安装的操作系统具有相同体系结构的远程工具。 换句话说，如果要在运行64位操作系统的远程计算机上调试32位应用程序，则必须在远程计算机上安装该远程工具的64位版本。  
  
3. 完成下载可执行文件后，请按照说明在远程计算机上安装该应用程序。 请参阅[安装说明](#bkmk_setup)

如果尝试将远程调试器（msvsmon）复制到远程计算机并运行它，请注意，仅当你下载这些工具时才安装**远程调试器配置向导**（**rdbgwiz.exe**），并且你可能需要使用向导进行配置，尤其是在你希望远程调试器作为服务运行时。 有关详细信息，请参阅下面的["（可选）将远程调试器配置为以下服务"](#bkmk_configureService) 。

### <a name="to-run-the-remote-debugger-from-a-file-share"></a>从文件共享运行远程调试器

你可以在已安装 Visual Studio 2015 社区版、专业版或企业版的计算机上找到远程调试器（**msvsmon**）。 在许多情况下，设置远程调试的最简单方法是从文件共享运行远程调试器（msvsmon）。 有关使用限制，请参阅远程调试器的帮助页（远程调试器中的**帮助/使用情况**）。

1. 在与你的 Visual Studio 版本匹配的目录中查找**msvsmon。** 对于 Visual Studio 2015：

      **Program Files\Microsoft Visual Studio 14.0 \ Common7\ide\remote debugger Debugger\x86\msvsmon.exe**
      
      **Program Files\Microsoft Visual Studio 14.0 \ Common7\ide\remote debugger Debugger\x64\msvsmon.exe**

2. 在 Visual Studio 计算机上共享**远程调试器**文件夹。

3. 在远程计算机上，运行**msvsmon**。 按照[安装说明](#bkmk_setup)进行操作。

> [!TIP] 
> 有关命令行安装和命令行参考，请参阅**msvsmon**的帮助页，方法是在安装了 Visual Studio 的计算机上的命令行中键入 ``msvsmon.exe /?`` （或在远程调试器中**使用 "帮助/使用**"）。

## <a name="supported-operating-systems"></a>Supported Operating Systems  
 远程计算机运行的是下列操作系统之一：  
  
- Windows 10  
  
- Windows 8 或 8.1  
  
- Windows 7 Service Pack 1  
  
- Windows Server 2012 或 Windows Server 2012 R2  
  
- Windows Server 2008 Service Pack 2、Windows Server 2008 R2 Service Pack 1  
  
## <a name="supported-hardware-configurations"></a>支持的硬件配置  
  
- 1.6 GHz 或更快的处理器  
  
- 1 GB 的 RAM（如果在虚拟机上运行则需 1.5 GB）  
  
- 1 GB 的可用硬盘空间  
  
- 5400 RPM 硬盘驱动器  
  
- DirectX 9 支持的视频卡，可在 1024 x 768 或更高版本的显示分辨率下运行  
  
## <a name="network-configuration"></a>网络配置  
 远程计算机与 Visual Studio 计算机必须通过网络、工作组、家庭组或其他通过以太网电缆直接连接的方式连接在一起。 不支持通过 Internet 进行调试。  
  
## <a name="bkmk_setup"></a>设置远程调试器  
 必须在远程计算机上具有管理权限  
  
1. 定位远程调试器应用程序。 （打开 "开始" 菜单并搜索 "**远程调试器**"。）
  
    如果在远程服务器上运行远程调试器，则可以右键单击远程调试器应用，然后选择 "以**管理员身份运行**" （或者，你可以将远程调试器作为服务运行）。如果未在远程服务器上运行，只需正常启动。
  
2. 首次启动远程工具时（或在配置之前），将显示 "**远程调试配置**对话框" 对话框。  
  
    ![RemoteDebuggerConfWizardPage](../debugger/media/remotedebuggerconfwizardpage.png "RemoteDebuggerConfWizardPage")  
  
3. 如果未安装 Windows 服务 API （仅在 Windows Server 2008 R2 上发生），请选择 "**安装**" 按钮。  
  
4. 选择你想要在上面使用远程工具的网络类型。 必须至少选择一种网络类型。 如果这些计算机通过域连接，则必须选择第一项。 如果这些计算机通过工作组或家庭组连接，你需要视情况选择第二或第三项。  
  
5. 选择 "**配置远程调试**"，配置防火墙并启动工具。  
  
6. 配置完成后，将显示远程调试器窗口。
  
    ![RemoteDebuggerWindow](../debugger/media/remotedebuggerwindow.png "RemoteDebuggerWindow")
  
    远程调试器正在等待连接。 记下显示的服务器名称和端口号，因为稍后要在 Visual Studio 中进行配置时需要用到它。  
  
   完成调试并且需要停止远程调试器后，请单击窗口上的 "**文件"/"退出**"。 你可以从 "**开始**" 菜单或从命令行重新启动它：  
  
   **\<Visual Studio 安装目录 > \Common7\IDE\Remote 调试器\\< x86、x64 或 Appx\msvsmon.exe**。  
  
## <a name="configure-the-remote-debugger"></a>配置远程调试器  
 首次启动后，你可以更改远程调试器的部分配置。
  
- 若要使其他用户能够连接到远程调试器，请选择 "**工具"/"权限**"。 你必须拥有管理员特权才能授予或拒绝权限。

  > [!IMPORTANT]
  > 您可以在与您在 Visual Studio 计算机上使用的用户帐户不同的用户帐户下运行远程调试器，但必须将不同的用户帐户添加到远程调试器的权限中。 

   或者，你可以从命令行启动远程调试器，其中 **/allow \<用户名 >** 参数： **msvsmon/allow \<username@computer>** 。
  
- 若要更改身份验证模式或端口号，或为远程工具指定超时值：请选择 "**工具"/"选项**"。  
  
   有关默认情况下使用的端口号列表，请参阅[远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)。  
  
   > [!WARNING]
  > 可以选择在“无身份验证”模式下运行远程工具，但强烈建议不要使用此模式。 在此模式下运行时，无法保证网络安全。 只有在确认网络不会遇到恶意通信的情况下，才可选择“无身份验证”模式。

## <a name="bkmk_configureService"></a>可有可无将远程调试器配置为服务
 对于在 ASP.NET 和其他服务器环境中进行调试，您必须以管理员身份运行远程调试器，或者，如果您希望它始终运行，请将远程调试器作为服务运行。
  
 如果要将远程调试器配置为服务，请执行以下步骤。  
  
1. 找到 “远程调试器配置向导”(rdbgwiz.exe)。 （这是一个独立于远程调试器的应用程序。）仅当安装远程工具时，该功能才可用。 它不与 Visual Studio 一起安装。  
  
2. 开始运行配置向导。 当第一页出现时，单击“下一步”。  
  
3. 勾选“将 Visual Studio 2015 远程调试器作为服务运行” 复选框。  
  
4. 添加用户帐户的名称和密码。  
  
    你可能需要将“作为服务登录” 的用户权限添加到此帐户。 （找到“启动” 页或窗口（或命令提示符下的类型 **secpol** ）中的 “本地安全策略”(secpol.msc)。 当显示窗口时，双击“用户权限分配”，然后在右窗格中找到 “作为服务登录”。 双击该选项。 将用户帐户添加到 "**属性**" 窗口，然后单击 **"确定"** 。）单击 "**下一步**"。  
  
5. 选择你希望远程工具与之通信的网络类型。 必须至少选择一种网络类型。 如果这些计算机通过域连接，则应选择第一项。 如果这些计算机通过工作组或家庭组连接，则应选择第二或第三项。 单击“下一步”。  
  
6. 如果可以启动服务，则会显示“你已成功完成 Visual Studio 远程调试器配置向导”。 如果无法启动服务，则会显示“未能完成 Visual Studio 远程调试器配置向导”。 此页还提供了为使服务正常启动要遵循的一些提示。  
  
7. 单击 **“完成”** 。  
  
   此时，远程调试器正作为服务运行。 你可以通过转到“控制面板”/“服务” 并找到“Visual Studio 2015 远程调试器”来对此进行验证。  
  
   你可以从“控制面板”/“服务”停止和启动远程调试器服务。  

## <a name="remote-debug-an-aspnet-application"></a>远程调试 ASP.NET 应用程序  
 将 ASP.NET 应用程序部署到运行 IIS 的远程计算机的步骤各不相同，具体取决于操作系统和 IIS 的版本。 对于运行 Windows Server 2008 或安装了 IIS 7.5 或更高版本的 Windows Server 2012 的远程计算机，请参阅远程[调试 ASP.NET 在远程 IIS 计算机上](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)。
 
 如果正在调试 ASP.NET Core 的应用，请参阅[发布到 IIS](https://docs.asp.net/en/latest/publishing/iis.html)。 若要在 IIS 上发布 ASP.NET Core，需要执行不同的步骤。 成功发布 ASP.NET Core 应用后，可以[像使用其他 ASP.NET 应用](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)一样对其进行远程调试，只不过需要附加到的进程是 dnx 而不是 w3wp.exe。

## <a name="remote-debug-a-visual-c-project"></a>远程调试 Visual C++ 项目  
 在下面的过程中，项目的名称和路径为 C:\remotetemp\MyMfc，远程计算机的名称为**MJO**。  
  
1. 创建名为 mymfc 的 MFC 应用程序。  
  
2. 在应用程序中容易到达的地方设置断点，例如，在 MainFrm.cpp 中（位于  **的开头）** `CMainFrame::OnCreate`。  
  
3. 在解决方案资源管理器中，右键单击项目，然后选择 "**属性**"。 打开“调试”选项卡。  
  
4. 将“要启动的调试器”更改为“远程 Windows 调试器”。  
  
    ![RemoteDebuggingCPlus](../debugger/media/remotedebuggingcplus.png "RemoteDebuggingCPlus")  
  
5. 对属性进行以下更改：  
  
   |设置|“值”|
   |-|-|  
   |远程命令|C:\remotetemp\mymfc.exe|  
   |工作目录|C:\remotetemp|  
   |“远程服务器名称”|MJO：*portnumber*|  
   |连接|带 Windows 身份验证的远程访问|  
   |调试器类型|仅限本机|  
   |部署目录|C:\remotetemp。|  
   |其他要部署的文件|C:\data\mymfcdata.txt。|  
  
    如果部署其他文件（可选），则该文件夹必须在两台计算机上都存在。  
  
6. 在解决方案资源管理器中，右键单击该解决方案，然后选择 " **Configuration Manager**"。  
  
7. 对于“调试”配置，请选中“部署”复选框。  
  
    ![RemoteDebugCplusDeploy](../debugger/media/remotedebugcplusdeploy.png "RemoteDebugCplusDeploy")  
  
8. 开始调试（"**调试"/"启动调试**" 或按**F5**）。  
  
9. 可执行文件会自动部署到远程计算机。  
  
10. 如果系统提示，请输入网络凭据以连接到远程计算机。  
  
     所需的凭据特定于你的网络安全配置。 例如，在域计算机上，您可以选择一个安全证书或输入您的域名和密码。 在非域计算机上，可以输入计算机名称和有效的用户帐户名称（如<strong>MJO-DL\name@something.com</strong>）以及正确的密码。  
  
11. 在 Visual Studio 计算机上，你应看到在断点处已停止执行。  
  
    > [!TIP]
    > 或者，你可以采用单独的步骤部署文件。 在“解决方案资源管理器”中，右键单击“mymfc”节点，然后选择“部署”。  
  
    如果具有需要由应用程序使用的非代码文件，则需要将其包含在 Visual Studio 项目中。 为其他文件创建项目文件夹（在**解决方案资源管理器**中，单击 "**添加/新建文件夹**"。）然后，将文件添加到该文件夹（在**解决方案资源管理器**中，单击 "**添加/现有项**"，然后选择文件。）。 在每个文件的“属性”页中，将“复制到输出目录”设置为“始终复制”。  
  
## <a name="remote-debug-a-visual-c-or-visual-basic-project"></a>远程调试 Visual C# 或 Visual Basic 项目  
 调试器不能将 Visual C# 或 Visual Basic 桌面应用程序部署到远程计算机，但你仍然可以按如下所示方法远程调试它们。 下面的过程假定您要在名为**MJO**的计算机上调试它，如前面的插图所示。
  
1. 创建一个名为“MyWpf”的 WPF 项目。  
  
2. 在代码中的某个容易到达的地方设置断点。  
  
    例如，可在按钮处理程序中设置断点。 为此，请打开 Mainwindow.xaml 并从 "工具箱" 中添加 "按钮" 控件，然后双击按钮以打开其处理程序。
  
3. 在“解决方案资源管理器”中，右键单击项目，然后选择“属性”。  
  
4. 在“属性”页上，选择"调试"选项卡。  
  
    ![RemoteDebuggerCSharp](../debugger/media/remotedebuggercsharp.png "RemoteDebuggerCSharp")  
  
5. 请确保“工作目录”文本框为空。  
  
6. 选择 "**使用远程计算机**"，然后在文本框中键入**MJO： 4020** 。 （4020是远程调试器窗口中显示的端口号）。  
  
7. 请确保未选中“启用本机代码调试”。  
  
8. 生成项目。  
  
9. 在远程计算机上创建一个文件夹，其路径与 Visual Studio 计算机上的调试文件夹相同：**source path>\MyWPF\MyWPF\bin\Debug** **\<** 。  
  
10. 将你刚才从 Visual Studio 计算机生成的可执行文件复制到远程计算机上新创建的文件夹。
  
    > [!CAUTION]
    > 不要对代码进行更改或重新生成（或必须重复此步骤）。 复制到远程计算机的可执行文件必须与你的本地源和符号完全匹配。

    可以手动复制项目，使用 Xcopy、Robocopy、Powershell 或其他选项。
  
11. 请确保远程调试器正在目标计算机上运行。 （如果不是，请在 "**开始**" 菜单中搜索 "**远程调试器**"。 ）远程调试器窗口如下所示。  
  
     ![RemoteDebuggerWindow](../debugger/media/remotedebuggerwindow.png "RemoteDebuggerWindow")  
  
12. 在 Visual Studio 中，启动调试（"**调试"/"启动调试**" 或按**F5**）。  
  
13. 如果系统提示，请输入网络凭据以连接到远程计算机。  
  
     所需的凭据因你的网络安全配置而异。 例如，你可以在域计算机上输入你的域名和密码。 在非域计算机上，可以输入计算机名称和有效的用户帐户名称（如<strong>MJO-DL\name@something.com</strong>）以及正确的密码。

     你应看到远程计算机上打开了 WPF 应用程序的主窗口。
  
14. 如有必要，请采取操作来命中断点。 你应看到该断点处于活动状态。 如果不是，则尚未加载应用程序的符号。 重试，如果这不起作用，请获取有关加载符号的信息，以及如何在[理解符号文件和 Visual Studio 的符号设置](https://devblogs.microsoft.com/devops/understanding-symbol-files-and-visual-studios-symbol-settings/)时排查它们的问题。
  
15. 在 Visual Studio 机器上，你应看到执行在断点处停止。
  
    如果具有需要由应用程序使用的非代码文件，则需要将其包含在 Visual Studio 项目中。 为其他文件创建项目文件夹（在**解决方案资源管理器**中，单击 "**添加/新建文件夹**"。）然后，将文件添加到该文件夹（在**解决方案资源管理器**中，单击 "**添加/现有项**"，然后选择文件。）。 在每个文件的“属性”页中，将“复制到输出目录”设置为“始终复制”。
  
## <a name="set-up-debugging-with-remote-symbols"></a>使用远程符号设置调试  
 你应能够使用你在 Visual Studio 计算机生成的符号调试你的代码。 使用本地符号时远程调试器的性能更佳。  如果必须使用远程符号，则需要告诉远程调试监视器以查找远程计算机上的符号。  
  
 从 Visual Studio 2013 Update 2 开始，你可以使用以下 msvsmon 命令行开关来使用用于托管代码的远程符号：`Msvsmon / /FallbackLoadRemoteManagedPdbs`  
  
 有关详细信息，请参阅远程调试帮助（在远程调试器窗口中按**F1** ，或单击 "**帮助/用法**"）。 有关详细信息，可以参阅 [Visual Studio 2012 和 2013 中的 .NET 远程符号加载更改](https://devblogs.microsoft.com/devops/net-remote-symbol-loading-changes-in-visual-studio-2012-and-2013/)  
  
## <a name="bkmk_winstoreAzure"></a>在 Windows 应用商店和 Azure 应用上进行远程调试  
 有关使用 Windows 应用商店应用进行远程调试的详细信息，请参阅[从 Visual Studio 调试和测试远程设备上的 Windows 应用商店应用](https://msdn.microsoft.com/library/windows/apps/hh441469.aspx)。  
  
 有关在 Azure 上进行调试的信息，请参阅以下主题之一：  
  
- [在 Visual Studio 中调试云服务或虚拟机](../azure/vs-azure-tools-debug-cloud-services-virtual-machines.md)  
  
- [在 Visual Studio 中调试 .NET 后端](https://blogs.msdn.microsoft.com/azuremobile/2014/03/14/debugging-net-backend-in-visual-studio/)  
  
- Azure 网站上的远程调试简介（[第 1](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/)部分、第[2](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)部分、第[3](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)部分）。  
  
## <a name="see-also"></a>请参阅  
 [在 Visual Studio 中进行调试](../debugger/debugging-in-visual-studio.md)   
 [配置 Windows 防火墙以便进行远程调试](../debugger/configure-the-windows-firewall-for-remote-debugging.md)   
 [Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)   
 [远程调试远程 IIS 计算机上的 ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)  
 [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)
