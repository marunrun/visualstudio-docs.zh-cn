---
title: Remote Debugging | Microsoft Docs
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
# <a name="remote-debugging"></a>Remote Debugging
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以调试已部署在另一台计算机的 Visual Studio 应用程序。  要进行此操作，可使用 Visual Studio 远程调试器。  
  
 此处的信息适用于 Windows 桌面应用程序和 ASP.NET 应用程序。  For information about remote debugging Windows Store apps and Azure apps, see [Remote Debugging on Windows Store and Azure apps](#bkmk_winstoreAzure).  
  
## <a name="get-the-remote-tools"></a>Get the remote tools  
You can either download the remote tools directly on the device or server that you want to debug, or you can get the remote tools from your host machine with Visual Studio installed.

### <a name="to-download-and-install-the-remote-tools"></a>To download and install the remote tools
  
1. On the device or server machine that you want to debug (rather than the machine running Visual Studio), get the correct version of the remote tools.

    |Version|链接|注意|
    |-|-|-|
    |Visual Studio 2015 Update 3|[远程工具](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|If prompted, join the free Visual Studio Dev Essentials group or you can just sign in with a valid Visual Studio subscription. Then re-open the link if necessary. Always download the version matching your device operating system (x86, x64, or  ARM version)|
    |Visual Studio 2015 (older)|[远程工具](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|If prompted, join the free Visual Studio Dev Essentials group or you can just sign in with a valid Visual Studio subscription. Then re-open the link if necessary.|
    |Visual Studio 2013|[远程工具](https://msdn.microsoft.com/library/bt727f1t(v=vs.120).aspx#BKMK_Installing_the_Remote_Tools)|Download page in Visual Studio 2013 documentation|
    |Visual Studio 2012|[远程工具](https://msdn.microsoft.com/library/bt727f1t(v=vs.110).aspx#BKMK_Installing_the_Remote_Tools)|Download page in Visual Studio 2012 documentation|
  
2. On the download page, choose the version of the tools that matches your operating system (x86, x64, or  ARM version) and download the remote tools.
  
    > [!IMPORTANT]
    > We recommend you install the most recent version of the remote tools that matches your version of Visual Studio. Mismatched versions are not recommended.  
    >   
    >  In addition, you must install the remote tools that have the same architecture as the operating system on which you want to install it. In other words, if you want to debug a 32-bit application on a remote computer running a 64-bit operating system, you must install the 64-bit version of the remote tools on the remote computer.  
  
3. 完成下载可执行文件后，请按照说明在远程计算机上安装该应用程序。 See [setup instructions](#bkmk_setup)

If you try to copy the remote debugger (msvsmon.exe) to the remote computer and run it, be aware that the **Remote Debugger Configuration Wizard** (**rdbgwiz.exe**) is installed only when you download the tools, and you may need to use the wizard for configuration later, especially if you want the remote debugger to run as a service. For more information, see [(Optional) Configure the remote debugger as a service](#bkmk_configureService) below.

### <a name="to-run-the-remote-debugger-from-a-file-share"></a>To run the remote debugger from a file share

You can find the remote debugger (**msvsmon.exe**) on a computer with Visual Studio 2015 Community, Professional, or Enterprise already installed. For many scenarios, the easiest way to set up remote debugging is to run the remote debugger (msvsmon.exe) from a file share. For usage limitations, see the remote debugger's Help page (**Help / Usage** in the remote debugger).

1. Find **msvsmon.exe** in the directory matching your version of Visual Studio. For Visual Studio 2015:

      **Program Files\Microsoft Visual Studio 14.0\Common7\IDE\Remote Debugger\x86\msvsmon.exe**
      
      **Program Files\Microsoft Visual Studio 14.0\Common7\IDE\Remote Debugger\x64\msvsmon.exe**

2. Share the **Remote Debugger** folder on the Visual Studio computer.

3. On the remote computer, run **msvsmon.exe**. Follow the [setup instructions](#bkmk_setup).

> [!TIP] 
> For command line installation and command line reference, see the Help page for **msvsmon.exe** by typing ``msvsmon.exe /?`` in the command line on the computer with Visual Studio installed (or go to **Help / Usage** in the remote debugger).

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
  
## <a name="bkmk_setup"></a>Set up the remote debugger  
 必须在远程计算机上具有管理权限  
  
1. 定位远程调试器应用程序。 (Open the Start menu and search for **Remote Debugger**.)
  
    If you are running the remote debugger on a  remote server, you can right-click the Remote Debugger app and choose **Run as administrator** (Or, you can run the remote debugger as a service).If you are not running it on a remote server, just start it normally.
  
2. When you start the remote tools for the first time (or before you have configured it), the **Remote Debugging Configuration** dalog box appears.  
  
    ![RemoteDebuggerConfWizardPage](../debugger/media/remotedebuggerconfwizardpage.png "RemoteDebuggerConfWizardPage")  
  
3. If the Windows Service API is not installed (which happens only on Windows Server 2008 R2), choose the **Install** button.  
  
4. 选择你想要在上面使用远程工具的网络类型。 必须至少选择一种网络类型。 如果这些计算机通过域连接，则必须选择第一项。 如果这些计算机通过工作组或家庭组连接，你需要视情况选择第二或第三项。  
  
5. Choose **Configure remote debugging** to configure the firewall and start the tool.  
  
6. 配置完成后，将显示远程调试器窗口。
  
    ![RemoteDebuggerWindow](../debugger/media/remotedebuggerwindow.png "RemoteDebuggerWindow")
  
    The remote debugger is now waiting for a connection. Make a note of the server name and port number that is displayed, because you will need this later for configuration in Visual Studio.  
  
   When you are finished debugging and need to stop the remote debugger, click **File / Exit** on the window. You can restart it from the **Start** menu or from the command line:  
  
   **\<Visual Studio installation directory>\Common7\IDE\Remote Debugger\\<x86, x64, or Appx\msvsmon.exe**.  
  
## <a name="configure-the-remote-debugger"></a>配置远程调试器  
 首次启动后，你可以更改远程调试器的部分配置。
  
- To enable other users to connect to the remote debugger, choose **Tools / Permissions**. 你必须拥有管理员特权才能授予或拒绝权限。

  > [!IMPORTANT]
  > You can run the remote debugger under a user account that differs from the user account you are using on the Visual Studio computer, but you must add the different user account to the remote debugger's permissions. 

   Alternatively, you can start the remote debugger from the command line with the **/allow \<username>** parameter: **msvsmon /allow \<username@computer** .
  
- To change the Authentication mode or the port number, or to specify a timeout value for the remote tools: choose **Tools / Options**.  
  
   For a listing of the port numbers used by default, see [Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md).  
  
   > [!WARNING]
  > 可以选择在“无身份验证”模式下运行远程工具，但强烈建议不要使用此模式。 在此模式下运行时，无法保证网络安全。 只有在确认网络不会遇到恶意通信的情况下，才可选择“无身份验证”模式。

## <a name="bkmk_configureService"></a> (Optional) Configure the remote debugger as a service
 For debugging in ASP.NET and other server environments, you must either run the remote debugger as an Administrator or, if you want it always running,  run the remote debugger as a service.
  
 If you want to configure the remote debugger as a service, follow these steps.  
  
1. 找到 “远程调试器配置向导”(rdbgwiz.exe)。 (This is a separate application from the Remote Debugger.) It is available only when you install the remote tools. 它不与 Visual Studio 一起安装。  
  
2. 开始运行配置向导。 当第一页出现时，单击“下一步”。  
  
3. 勾选“将 Visual Studio 2015 远程调试器作为服务运行” 复选框。  
  
4. 添加用户帐户的名称和密码。  
  
    你可能需要将“作为服务登录” 的用户权限添加到此帐户。 （找到“启动” 页或窗口（或命令提示符下的类型 **secpol** ）中的 “本地安全策略”(secpol.msc)。 当显示窗口时，双击“用户权限分配”，然后在右窗格中找到 “作为服务登录”。 双击该选项。 Add the user account to the **Properties** window and click **OK**.) Click **Next**.  
  
5. 选择你希望远程工具与之通信的网络类型。 必须至少选择一种网络类型。 如果这些计算机通过域连接，则应选择第一项。 如果这些计算机通过工作组或家庭组连接，则应选择第二或第三项。 单击 **“下一步”** 。  
  
6. 如果可以启动服务，则会显示“你已成功完成 Visual Studio 远程调试器配置向导”。 如果无法启动服务，则会显示“未能完成 Visual Studio 远程调试器配置向导”。 此页还提供了为使服务正常启动要遵循的一些提示。  
  
7. 单击 **“完成”** 。  
  
   此时，远程调试器正作为服务运行。 你可以通过转到“控制面板”/“服务” 并找到“Visual Studio 2015 远程调试器”来对此进行验证。  
  
   你可以从“控制面板”/“服务”停止和启动远程调试器服务。  

## <a name="remote-debug-an-aspnet-application"></a>远程调试 ASP.NET 应用程序  
 将 ASP.NET 应用程序部署到运行 IIS 的远程计算机的步骤各不相同，具体取决于操作系统和 IIS 的版本。 For remote computers running Windows Server 2008 or Windows Server 2012 that have IIS 7.5 or later installed, please see [Remote Debugging ASP.NET on a Remote IIS Computer](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md).
 
 If you are debugging an ASP.NET Core app, please see [Publishing to IIS](https://docs.asp.net/en/latest/publishing/iis.html). Different steps are required to publish an ASP.NET Core on IIS. Once you publish an ASP.NET Core app successfully, you can remote debug it [just like other ASP.NET apps](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md), except that the process you need to attach to is dnx.exe instead of w3wp.exe.

## <a name="remote-debug-a-visual-c-project"></a>远程调试 Visual C++ 项目  
 In the following procedure, the name and path of the project is C:\remotetemp\MyMfc, and the name of the remote computer is **MJO-DL**.  
  
1. 创建名为 mymfc 的 MFC 应用程序。  
  
2. 在应用程序中容易到达的地方设置断点，例如，在 MainFrm.cpp 中（位于 `CMainFrame::OnCreate` 的开头）。  
  
3. In Solution Explorer, right-click on the project and select **Properties**. 打开“调试”选项卡。  
  
4. 将“要启动的调试器”更改为“远程 Windows 调试器”。  
  
    ![RemoteDebuggingCPlus](../debugger/media/remotedebuggingcplus.png "RemoteDebuggingCPlus")  
  
5. 对属性进行以下更改：  
  
   |设置|“值”|
   |-|-|  
   |远程命令|C:\remotetemp\mymfc.exe|  
   |工作目录|C:\remotetemp|  
   |远程服务器名称|MJO-DL:*portnumber*|  
   |连接|带 Windows 身份验证的远程访问|  
   |调试器类型|仅限本机|  
   |部署目录|C:\remotetemp。|  
   |其他要部署的文件|C:\data\mymfcdata.txt。|  
  
    If you deploy additional files (optional), the folder must exist on both machines.  
  
6. In Solution Explorer, right-click the solution and choose **Configuration Manager**.  
  
7. 对于“调试”配置，请选中“部署”复选框。  
  
    ![RemoteDebugCplusDeploy](../debugger/media/remotedebugcplusdeploy.png "RemoteDebugCplusDeploy")  
  
8. Start debugging (**Debug / Start Debugging**, or **F5**).  
  
9. 可执行文件会自动部署到远程计算机。  
  
10. If prompted, enter network credentials to connect to the remote machine.  
  
     The required credentials are specific to your network's security configuration. For example, on a domain computer, you might choose a security certificate or enter your domain name and password. On a non-domain machine, you might enter the machine name and a valid user account name, like <strong>MJO-DL\name@something.com</strong>, along with the correct password.  
  
11. 在 Visual Studio 计算机上，你应看到在断点处已停止执行。  
  
    > [!TIP]
    > 或者，你可以采用单独的步骤部署文件。 在“解决方案资源管理器”中，右键单击“mymfc”节点，然后选择“部署”。  
  
    如果具有需要由应用程序使用的非代码文件，则需要将其包含在 Visual Studio 项目中。 Create a project folder for the additional files (in the **Solution Explorer**, click **Add / New Folder**.) Then add the files to the folder (in the **Solution Explorer**, click **Add / Existing Item**, then select the files.). 在每个文件的“属性”页中，将“复制到输出目录”设置为“始终复制”。  
  
## <a name="remote-debug-a-visual-c-or-visual-basic-project"></a>远程调试 Visual C# 或 Visual Basic 项目  
 调试器不能将 Visual C# 或 Visual Basic 桌面应用程序部署到远程计算机，但你仍然可以按如下所示方法远程调试它们。 The following procedure assumes that you want to debug it on a computer named **MJO-DL**, as shown in the earlier illustration.
  
1. 创建一个名为“MyWpf”的 WPF 项目。  
  
2. 在代码中的某个容易到达的地方设置断点。  
  
    例如，可在按钮处理程序中设置断点。 To do this, open MainWindow.xaml, and add a Button control from the Toolbox, then double-click the button to open it's handler.
  
3. 在“解决方案资源管理器”中，右键单击项目，然后选择“属性”。  
  
4. 在“属性”页上，选择"调试"选项卡。  
  
    ![RemoteDebuggerCSharp](../debugger/media/remotedebuggercsharp.png "RemoteDebuggerCSharp")  
  
5. 请确保“工作目录”文本框为空。  
  
6. Choose **Use remote machine**, and type **MJO-DL:4020** in the text box. (4020 is the port number shown in the remote debugger window).  
  
7. 请确保未选中“启用本机代码调试”。  
  
8. 生成项目。  
  
9. 在远程计算机上创建一个文件夹，其路径与 Visual Studio 计算机上的调试文件夹相同：\<source path>\MyWPF\MyWPF\bin\Debug。  
  
10. 将你刚才从 Visual Studio 计算机生成的可执行文件复制到远程计算机上新创建的文件夹。
  
    > [!CAUTION]
    > Do not make changes to the code or rebuild (or you must repeat this step). 复制到远程计算机的可执行文件必须与你的本地源和符号完全匹配。

    You can copy the project manually, use Xcopy, Robocopy, Powershell, or other options.
  
11. Make sure the remote debugger is running on the target machine. (If it's not, search for **Remote Debugger** in the **Start** menu. ) The remote debugger window looks like this.  
  
     ![RemoteDebuggerWindow](../debugger/media/remotedebuggerwindow.png "RemoteDebuggerWindow")  
  
12. In Visual Studio, start debugging (**Debug / Start Debugging**, or **F5**).  
  
13. If prompted, enter network credentials to connect to the remote machine.  
  
     The required credentials vary depending on your network's security configuration. For example, on a domain computer, you can  enter your domain name and password. On a non-domain machine, you might enter the machine name and a valid user account name, like <strong>MJO-DL\name@something.com</strong>, along with the correct password.

     你应看到远程计算机上打开了 WPF 应用程序的主窗口。
  
14. If necessary, take action to hit the breakpoint. 你应看到该断点处于活动状态。 如果不是，则尚未加载应用程序的符号。 Retry, and if that doesn't work, get information about loading symbols and how troubleshoot them at [Understanding symbol files and Visual Studio’s symbol settings](https://devblogs.microsoft.com/devops/understanding-symbol-files-and-visual-studios-symbol-settings/).
  
15. 在 Visual Studio 机器上，你应看到执行在断点处停止。
  
    如果具有需要由应用程序使用的非代码文件，则需要将其包含在 Visual Studio 项目中。 Create a project folder for the additional files (in the **Solution Explorer**, click **Add / New Folder**.) Then add the files to the folder (in the **Solution Explorer**, click **Add / Existing Item**, then select the files.). 在每个文件的“属性”页中，将“复制到输出目录”设置为“始终复制”。
  
## <a name="set-up-debugging-with-remote-symbols"></a>使用远程符号设置调试  
 你应能够使用你在 Visual Studio 计算机生成的符号调试你的代码。 使用本地符号时远程调试器的性能更佳。  如果必须使用远程符号，则需要告诉远程调试监视器以查找远程计算机上的符号。  
  
 从 Visual Studio 2013 Update 2 开始，你可以使用以下 msvsmon 命令行开关来使用用于托管代码的远程符号：`Msvsmon / /FallbackLoadRemoteManagedPdbs`  
  
 For more information, please see the remote debugging help (press **F1** in the remote debugger window, or click **Help / Usage**). 有关详细信息，可以参阅 [Visual Studio 2012 和 2013 中的 .NET 远程符号加载更改](https://devblogs.microsoft.com/devops/net-remote-symbol-loading-changes-in-visual-studio-2012-and-2013/)  
  
## <a name="bkmk_winstoreAzure"></a> Remote Debugging on Windows Store and Azure apps  
 For information about remote debugging with Windows Store apps, see [Debug and test Windows Store apps on a remote device from Visual Studio](https://msdn.microsoft.com/library/windows/apps/hh441469.aspx).  
  
 有关在 Azure 上进行调试的信息，请参阅以下主题之一：  
  
- [Debugging a Cloud Service or Virtual Machine in Visual Studio](../azure/vs-azure-tools-debug-cloud-services-virtual-machines.md)  
  
- [Debugging the .NET Backend in Visual Studio](https://blogs.msdn.microsoft.com/azuremobile/2014/03/14/debugging-net-backend-in-visual-studio/)  
  
- Introduction to Remote Debugging on Azure Web Sites ([Part 1](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/), [Part 2](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/), [Part 3](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)).  
  
## <a name="see-also"></a>请参阅  
 [在 Visual Studio 中进行调试](../debugger/debugging-in-visual-studio.md)   
 [配置 Windows 防火墙以便进行远程调试](../debugger/configure-the-windows-firewall-for-remote-debugging.md)   
 [Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)   
 [远程调试远程 IIS 计算机上的 ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)  
 [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)
