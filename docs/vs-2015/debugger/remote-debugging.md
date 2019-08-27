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
ms.openlocfilehash: e31d177a8bda5435c2201701241638cb919cf9ec
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687549"
---
# <a name="remote-debugging"></a>Remote Debugging
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以调试已部署在另一台计算机的 Visual Studio 应用程序。  要进行此操作，可使用 Visual Studio 远程调试器。  
  
 此处的信息适用于 Windows 桌面应用程序和 ASP.NET 应用程序。  有关远程调试 Windows 应用商店应用程序和 Azure 应用程序的信息，请参阅[在 Windows 应用商店和 Azure 应用上进行远程调试](#bkmk_winstoreAzure)。  
  
## <a name="get-the-remote-tools"></a>获取远程工具  
你可以直接在设备或想要调试，或您的服务器上的远程工具可以安装了 Visual studio 从主机获取远程工具下载。

### <a name="to-download-and-install-the-remote-tools"></a>若要下载并安装远程工具
  
1. 在设备或服务器您想要调试的计算机 （而不运行 Visual Studio 的计算机），获取远程工具的正确版本。

    |Version|链接|说明|
    |-|-|-|
    |Visual Studio 2015 Update 3|[远程工具](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|如果系统提示，请加入免费的 Visual Studio Dev Essentials 组，或只是可以使用有效的 Visual Studio 订阅登录。 如有必要然后重新打开该链接。 请务必下载匹配您设备的操作系统 (x 86、 x64 或 ARM 版本） 的版本|
    |Visual Studio 2015 （较旧）|[远程工具](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|如果系统提示，请加入免费的 Visual Studio Dev Essentials 组，或只是可以使用有效的 Visual Studio 订阅登录。 如有必要然后重新打开该链接。|
    |Visual Studio 2013|[远程工具](https://msdn.microsoft.com/library/bt727f1t(v=vs.120).aspx#BKMK_Installing_the_Remote_Tools)|下载 Visual Studio 2013 文档中的页|
    |Visual Studio 2012|[远程工具](https://msdn.microsoft.com/library/bt727f1t(v=vs.110).aspx#BKMK_Installing_the_Remote_Tools)|下载 Visual Studio 2012 文档中的页|
  
2. 在下载页上，选择与匹配 (x 86、 x64 或 ARM 版本） 操作系统的版本的工具和下载远程工具。
  
    > [!IMPORTANT]
    > 我们建议安装最新版本的远程工具与你的 Visual Studio 版本匹配。 不建议版本不匹配。  
    >   
    >  此外，必须安装具有相同的体系结构作为你想要将其安装操作系统的远程工具。 换而言之，如果你想要调试远程计算机运行 64 位操作系统上的 32 位应用程序，您必须在远程计算机上安装远程工具的 64 位版本。  
  
3. 完成下载可执行文件后，请按照说明在远程计算机上安装该应用程序。 请参阅[安装说明进行操作](#bkmk_setup)

如果你尝试将远程调试器 (msvsmon.exe) 复制到远程计算机并运行它，请注意，**远程调试器配置向导**(**rdbgwiz.exe**) 仅在你下载时，才安装工具和你可能需要使用该向导配置更高版本，尤其是如果你想将远程调试器作为服务运行。 有关详细信息，请参阅[（可选） 配置远程调试器作为服务](#bkmk_configureService)下面。

### <a name="to-run-the-remote-debugger-from-a-file-share"></a>若要从文件共享运行远程调试器

您可以找到远程调试器 (**msvsmon.exe**) 使用 Visual Studio 2015 Community、 Professional 或 Enterprise 已安装的计算机上。 对于许多方案，设置远程调试的最简单方法是从文件共享运行远程调试器 (msvsmon.exe)。 有关使用情况的限制，请参阅远程调试器的帮助页 (**帮助 / 用法**远程调试器中)。

1. 查找**msvsmon.exe**匹配你的 Visual Studio 版本的目录中。 用于 Visual Studio 2015:

      **Program Files\Microsoft Visual Studio 14.0\Common7\IDE\Remote Debugger\x86\msvsmon.exe**
      
      **Program Files\Microsoft Visual Studio 14.0\Common7\IDE\Remote Debugger\x64\msvsmon.exe**

2. 共享**远程调试器**Visual Studio 计算机上的文件夹。

3. 在远程计算机上运行**msvsmon.exe**。 请按照[安装说明进行操作](#bkmk_setup)。

> [!TIP] 
> 命令行安装和命令行参考，请参阅的帮助页**msvsmon.exe**通过键入``msvsmon.exe /?``在安装了 Visual studio 计算机上的命令行中 (或转到**帮助 / 用法**远程调试器中)。

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
  
1. 定位远程调试器应用程序。 (打开开始菜单并搜索**远程调试器**。)
  
    如果远程服务器上运行远程调试器，可以右键单击远程调试器应用并选择**以管理员身份运行**（或者，可以作为服务运行远程调试器）。如果你不远程服务器上运行它，只是它正常启动。
  
2. 当启动远程工具，在第一次 （或之前对其进行配置），则**远程调试配置**对话框框中显示。  
  
    ![RemoteDebuggerConfWizardPage](../debugger/media/remotedebuggerconfwizardpage.png "RemoteDebuggerConfWizardPage")  
  
3. 如果 Windows 服务 API 未安装 （这仅在 Windows Server 2008 R2 时发生），选择**安装**按钮。  
  
4. 选择你想要在上面使用远程工具的网络类型。 必须至少选择一种网络类型。 如果这些计算机通过域连接，则必须选择第一项。 如果这些计算机通过工作组或家庭组连接，你需要视情况选择第二或第三项。  
  
5. 选择**配置远程调试**配置防火墙并启动该工具。  
  
6. 配置完成后，将显示远程调试器窗口。
  
    ![RemoteDebuggerWindow](../debugger/media/remotedebuggerwindow.png "RemoteDebuggerWindow")
  
    远程调试器现在正在等待连接。 请记下的服务器名称和端口号显示，因为您将需要此更高版本的 Visual Studio 中配置。  
  
   完成调试，需要停止远程调试器后，，单击**文件 / 退出**窗口上。 您可以重新启动它从**启动**菜单或从命令行：  
  
   **\<Visual Studio 安装目录 > \Common7\IDE\Remote 调试器\\< x86，x64，or Appx\msvsmon.exe**。  
  
## <a name="configure-the-remote-debugger"></a>配置远程调试器  
 首次启动后，你可以更改远程调试器的部分配置。
  
- 若要使其他用户能够连接到远程调试器，请选择**工具 / 权限**。 你必须拥有管理员特权才能授予或拒绝权限。

  > [!IMPORTANT]
  > 您可以从 Visual Studio 计算机所使用的用户帐户运行远程调试器在不同的用户帐户下，但必须将其他用户帐户添加到远程调试器的权限。 

   或者，可以从命令行启动远程调试器 **/allow\<用户名 >** 参数： **msvsmon /allow \< username@computer>**。
  
- 若要更改身份验证模式或端口号，或指定的远程工具的超时值： 选择**工具 / 选项**。  
  
   默认情况下使用的端口号的列表，请参阅[Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)。  
  
   > [!WARNING]
  > 可以选择在“无身份验证”模式下运行远程工具，但强烈建议不要使用此模式。 在此模式下运行时，无法保证网络安全。 只有在确认网络不会遇到恶意通信的情况下，才可选择“无身份验证”模式。

## <a name="bkmk_configureService"></a> （可选）配置远程调试器作为服务
 用于调试 ASP.NET 和其他服务器环境中，您必须以管理员身份运行远程调试器或时，如果希望始终运行，作为服务运行远程调试器。
  
 如果你想要配置远程调试器作为服务，请按照下列步骤。  
  
1. 找到  “远程调试器配置向导”(rdbgwiz.exe)。 （这是独立于远程调试器的应用程序。）仅在你安装远程工具后，它才可用。 它不与 Visual Studio 一起安装。  
  
2. 开始运行配置向导。 当第一页出现时，单击“下一步” 。  
  
3. 勾选“将 Visual Studio 2015 远程调试器作为服务运行”  复选框。  
  
4. 添加用户帐户的名称和密码。  
  
    你可能需要将“作为服务登录”  的用户权限添加到此帐户。 （找到“启动”  页或窗口（或命令提示符下的类型 **secpol** ）中的  “本地安全策略”(secpol.msc)。 当显示窗口时，双击“用户权限分配” ，然后在右窗格中找到  “作为服务登录”。 双击该选项。 将用户帐户添加到**属性**窗口，然后单击**确定**。)单击“下一步” 。  
  
5. 选择你希望远程工具与之通信的网络类型。 必须至少选择一种网络类型。 如果这些计算机通过域连接，则应选择第一项。 如果这些计算机通过工作组或家庭组连接，则应选择第二或第三项。 单击 **“下一步”**。  
  
6. 如果可以启动服务，则会显示 “你已成功完成 Visual Studio 远程调试器配置向导”。 如果无法启动服务，则会显示“未能完成 Visual Studio 远程调试器配置向导” 。 此页还提供了为使服务正常启动要遵循的一些提示。  
  
7. 单击 **“完成”**。  
  
   此时，远程调试器正作为服务运行。 你可以通过转到“控制面板”/“服务”  并找到 “Visual Studio 2015 远程调试器”来对此进行验证。  
  
   你可以从“控制面板”/“服务” 停止和启动远程调试器服务。  

## <a name="remote-debug-an-aspnet-application"></a>远程调试 ASP.NET 应用程序  
 将 ASP.NET 应用程序部署到运行 IIS 的远程计算机的步骤各不相同，具体取决于操作系统和 IIS 的版本。 对于远程计算机运行 Windows Server 2008 或 Windows Server 2012 具有 IIS 7.5 或更高版本安装，请参阅[Remote Debugging ASP.NET on a Remote IIS Computer](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)。
 
 如果你正在调试 ASP.NET Core 应用，请参阅[发布到 IIS](https://docs.asp.net/en/latest/publishing/iis.html)。 将发布在 IIS 上 ASP.NET Core 所需采取不同的步骤。 一旦您已成功发布 ASP.NET Core 应用，你可以远程连接对其进行调试[就像其他 ASP.NET 应用](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)，只不过您需要将附加到的进程是 dnx.exe 而不是 w3wp.exe。

## <a name="remote-debug-a-visual-c-project"></a>远程调试 Visual C++ 项目  
 在下面的过程的名称和项目的路径是 C:\remotetemp\MyMfc，且远程计算机的名称是**MJO DL**。  
  
1. 创建名为 mymfc 的 MFC 应用程序。  
  
2. 在应用程序中容易到达的地方设置断点，例如，在 MainFrm.cpp 中（位于 `CMainFrame::OnCreate` 的开头）。  
  
3. 在解决方案资源管理器中右键单击项目并选择**属性**。 打开“调试”选项卡。  
  
4. 将“要启动的调试器”更改为“远程 Windows 调试器”。  
  
    ![RemoteDebuggingCPlus](../debugger/media/remotedebuggingcplus.png "RemoteDebuggingCPlus")  
  
5. 对属性进行以下更改：  
  
   |设置|值|
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
  
8. 开始调试 (**调试 / 启动调试**，或**F5**)。  
  
9. 可执行文件会自动部署到远程计算机。  
  
10. 如果系统提示，请输入网络凭据以连接到远程计算机。  
  
     特定于网络的安全配置所需的凭据。 例如，可能的域计算机上，选择安全证书或输入你的域名和密码。 在非域计算机上，你可能会输入计算机名称和有效的用户帐户名称，如<strong>MJO-DL\name@something.com</strong>，以及正确的密码。  
  
11. 在 Visual Studio 计算机上，你应看到在断点处已停止执行。  
  
    > [!TIP]
    > 或者，你可以采用单独的步骤部署文件。 在“解决方案资源管理器”中，右键单击“mymfc”节点，然后选择“部署”。  
  
    如果具有需要由应用程序使用的非代码文件，则需要将其包含在 Visual Studio 项目中。 创建其他文件的项目文件夹 (在**解决方案资源管理器**，单击**添加 / 新建文件夹**。)然后将文件添加到的文件夹 (在**解决方案资源管理器**，单击**添加 / 现有项**，然后选择的文件。)。 在每个文件的“属性”页中，将“复制到输出目录”设置为“始终复制”。  
  
## <a name="remote-debug-a-visual-c-or-visual-basic-project"></a>远程调试 Visual C# 或 Visual Basic 项目  
 调试器不能将 Visual C# 或 Visual Basic 桌面应用程序部署到远程计算机，但你仍然可以按如下所示方法远程调试它们。 以下过程假设你想要在名为的计算机上调试它**MJO DL**前, 一张图中所示。
  
1. 创建一个名为“MyWpf”的 WPF 项目。  
  
2. 在代码中的某个容易到达的地方设置断点。  
  
    例如，可在按钮处理程序中设置断点。 若要执行此操作，打开 MainWindow.xaml，然后添加一个按钮控件从工具箱中，双击按钮以打开它的处理程序。
  
3. 在解决方案资源管理器，右键单击该项目并选择**属性**。  
  
4. 在“属性”页上，选择"调试"选项卡。  
  
    ![RemoteDebuggerCSharp](../debugger/media/remotedebuggercsharp.png "RemoteDebuggerCSharp")  
  
5. 请确保“工作目录”文本框为空。  
  
6. 选择**使用远程计算机**，然后键入**MJO-DL:4020**在文本框中。 （4020 是远程调试器窗口中显示的端口号）。  
  
7. 请确保未选中“启用本机代码调试”。  
  
8. 生成项目。  
  
9. 在远程计算机上创建一个文件夹，其路径与 Visual Studio 计算机上的调试文件夹相同：\<source path>\MyWPF\MyWPF\bin\Debug。  
  
10. 将你刚才从 Visual Studio 计算机生成的可执行文件复制到远程计算机上新创建的文件夹。
  
    > [!CAUTION]
    > 对代码或重新生成不会进行任何更改 （或必须重复此步骤）。 复制到远程计算机的可执行文件必须与你的本地源和符号完全匹配。

    可以手动复制该项目，使用 Xcopy、 Robocopy、 Powershell 或其他选项。
  
11. 请确保在目标计算机上运行远程调试器。 (如果不是，搜索**远程调试器**中**启动**菜单。 ） 在远程调试器窗口外观如下所示。  
  
     ![RemoteDebuggerWindow](../debugger/media/remotedebuggerwindow.png "RemoteDebuggerWindow")  
  
12. 在 Visual Studio 中，开始调试 (**调试 / 启动调试**，或**F5**)。  
  
13. 如果系统提示，请输入网络凭据以连接到远程计算机。  
  
     所需的凭据会有所不同，具体取决于网络的安全配置。 例如，在域的计算机，可以输入你的域名和密码。 在非域计算机上，你可能会输入计算机名称和有效的用户帐户名称，如<strong>MJO-DL\name@something.com</strong>，以及正确的密码。

     你应看到远程计算机上打开了 WPF 应用程序的主窗口。
  
14. 如果有必要，请采取措施以命中断点。 你应看到该断点处于活动状态。 如果不是，则尚未加载应用程序的符号。 重试，并且如果这不起作用，获取有关加载符号的信息和如何解决在这些问题[了解符号文件和 Visual Studio 的符号设置](http://blogs.msdn.com/b/visualstudioalm/archive/2015/01/05/understanding-symbol-files-and-visual-studio-s-symbol-settings.aspx)。
  
15. 在 Visual Studio 机器上，你应看到执行在断点处停止。
  
    如果具有需要由应用程序使用的非代码文件，则需要将其包含在 Visual Studio 项目中。 创建其他文件的项目文件夹 (在**解决方案资源管理器**，单击**添加 / 新建文件夹**。)然后将文件添加到的文件夹 (在**解决方案资源管理器**，单击**添加 / 现有项**，然后选择的文件。)。 在每个文件的“属性”页中，将“复制到输出目录”设置为“始终复制”。
  
## <a name="set-up-debugging-with-remote-symbols"></a>使用远程符号设置调试  
 你应能够使用你在 Visual Studio 计算机生成的符号调试你的代码。 使用本地符号时远程调试器的性能更佳。  如果必须使用远程符号，则需要告诉远程调试监视器以查找远程计算机上的符号。  
  
 从 Visual Studio 2013 Update 2 开始，你可以使用以下 msvsmon 命令行开关来使用用于托管代码的远程符号：`Msvsmon / /FallbackLoadRemoteManagedPdbs`  
  
 有关详细信息，请参阅远程调试帮助 (按**F1**中的远程调试器窗口中或单击**帮助 / 用法**)。 有关详细信息，可以参阅 [Visual Studio 2012 和 2013 中的 .NET 远程符号加载更改](http://blogs.msdn.com/b/visualstudioalm/archive/2013/10/16/net-remote-symbol-loading-changes-in-visual-studio-2012-and-2013.aspx)  
  
## <a name="bkmk_winstoreAzure"></a> 在 Windows 应用商店和 Azure 应用上进行远程调试  
 有关使用 Windows 应用商店应用程序进行远程调试的信息，请参阅[调试和测试 Windows 应用商店应用程序从 Visual Studio 在远程设备上的](https://msdn.microsoft.com/library/windows/apps/hh441469.aspx)。  
  
 有关在 Azure 上进行调试的信息，请参阅以下主题之一：  
  
- [调试云服务或在 Visual Studio 中的虚拟机](../azure/vs-azure-tools-debug-cloud-services-virtual-machines.md)  
  
- [调试 Visual Studio 中的.NET 后端](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx)  
  
- Azure 网站上的远程调试简介 ([第 1 部分](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/)，[第 2 部分](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)，[第 3 部分](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/))。  
  
## <a name="see-also"></a>请参阅  
 [在 Visual Studio 中进行调试](../debugger/debugging-in-visual-studio.md)   
 [配置 Windows 防火墙以便进行远程调试](../debugger/configure-the-windows-firewall-for-remote-debugging.md)   
 [Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)   
 [远程调试远程 IIS 计算机上的 ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)  
 [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)
