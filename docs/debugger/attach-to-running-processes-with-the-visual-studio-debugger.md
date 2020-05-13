---
title: 使用 Visual Studio 调试器附加到正在运行的进程 | Microsoft Docs
ms.custom: seodec18
ms.date: 04/14/2020
ms.topic: conceptual
f1_keywords:
- vs.debug.processes.attach
- vs.debug.process
- vs.debug.programs
- vs.debug.detaching
- vs.debug.processes
- vs.debug.error.attach
- vs.debug.remotemachine
dev_langs:
- CSharp
- FSharp
- C++
- VB
helpviewer_keywords:
- remote debugging, attaching to programs
- processes, attaching to running processes
- Attach to Process dialog box
- debugging [Visual Studio], attaching to processes
- debugger, processes
ms.assetid: 27900e58-090c-4211-a309-b3e1496d5824
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 075f5b0df703e31ea265085f422567a4fb5298a4
ms.sourcegitcommit: cc58ca7ceae783b972ca25af69f17c9f92a29fc2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "81385484"
---
# <a name="attach-to-running-processes-with-the-visual-studio-debugger"></a>使用 Visual Studio 调试器附加到运行的进程
你可将 Visual Studio 调试器附加到正在本地或远程计算机上运行的进程上。 进程运行后，选择 **"调试** > **附加到进程"** 或在可视化工作室中按**Ctrl**+**Alt**+**P，** 并使用 **"附加到进程"** 对话框将调试器附加到进程。

可以使用“附加到进程” 来调试本地或远程计算机上正在运行的应用、同时调试多个进程、 调试并非在 Visual Studio 中创建的应用或未使用附带调试器从 Visual Studio 启动的任何应用****。 例如，如果运行的是不带调试器的应用，并触发异常，则可以将调试器附加到运行应用的进程并开始调试。

> [!TIP]
> 不确定自己的调试方案是否需要使用“附加到进程”****？ 请参阅[常见调试方案](#BKMK_Scenarios)。

## <a name="attach-to-a-running-process-on-your-local-machine"></a><a name="BKMK_Attach_to_a_running_process"></a> 附加到本地计算机上正在运行的进程

要快速重新附加到以前附加到的进程，请参阅[重新附加到进程](#BKMK_reattach)。

要在远程计算机上调试进程，请参阅[附加到远程计算机上的进程](#BKMK_Attach_to_a_process_on_a_remote_computer)。

::: moniker range=">= vs-2019"
要在 Linux Docker 容器上调试 .NET Core 进程，请参阅[附加到 Linux Docker 容器](#BKMK_Linux_Docker_Attach)。
::: moniker-end

若要附加到本地计算机上的进程，请执行以下操作：****

1. 在可视化工作室中，选择**调试** > **附加到进程**（或按**Ctrl**+**Alt**+**P）** 以打开 **"附加到进程**"对话框。

   “连接类型”应设置为“默认”********。 “连接目标”应该是本地计算机名称****。

   ![DBG_Basics_Attach_To_Process](../debugger/media/DBG_Basics_Attach_To_Process.png "DBG_Basics_Attach_To_Process")

2. 在“可用进程”列表中，查找并选择要附加到的一个或多个进程****。

   - 若要快速选择一个进程，请在“筛选进程”框中键入其名称或首字母****。

   - 如果不知道进程名称，请浏览列表或参阅[常见调试方案](#BKMK_Scenarios)，了解一些常见的进程名称。

   >[!TIP]
   >“附加到进程”对话框处于打开状态时，进程可以在后台启动和停止，因此正在运行的进程列表可能不总是最新内容****。 可随时选择“刷新”查看当前列表****。

3. 在“附加到”字段中，确保已列出计划调试的代码类型****。 默认的“自动”设置适用于大多数应用类型****。

   要手动选择代码类型：
   1. 单击“选择”  。
   1. 在“选择代码类型”对话框中，选择“调试这些代码类型”********。
   1. 选择要调试的代码类型。
   1. 选择“确定”  。

4. 选择“附加”。****

>[!NOTE]
>可附加到多个应用进行调试，但在调试器中一次只能有一个应用处于活动状态。 可在 Visual Studio 的“调试位置”工具栏或“进程”窗口中设置活动的应用********。

## <a name="attach-to-a-process-on-a-remote-computer"></a><a name="BKMK_Attach_to_a_process_on_a_remote_computer"></a>附加到远程计算机上的进程

还可以在“附加到进程”对话框中选择远程计算机，查看该计算机上运行的可用进程列表，并附加到一个或多个进程以进行调试****。 远程调试器 (msvsmon.exe) 必须在远程计算机上运行**。 有关详细信息，请参阅[远程调试](../debugger/remote-debugging.md)。

有关调试已部署到 IIS 的应用程序ASP.NET的更多完整说明，请参阅[远程 IIS 计算机上的远程调试ASP.NET。](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)

**要附加到远程计算机上的正在运行的进程，请：**

1. 在可视化工作室中，选择**调试** > **附加到进程**（或按**Ctrl**+**Alt**+**P）** 以打开 **"附加到进程**"对话框。

2. 在大多数情况下，“连接类型”应为“默认”********。 在“连接目标”框中，使用以下方法之一选择远程计算机****：

   - 选择下拉箭头旁边的“连接目标”，并从下拉列表中选择计算机名称****。
   - 在 **"连接"目标**框中键入计算机名称，然后按**Enter**。

     验证 Visual Studio 是否将所需的端口添加到计算机名称，该端口以格式显示：**\<远程计算机名称>：端口**

     ::: moniker range=">= vs-2019"

     > [!NOTE]
     > 如果无法使用远程计算机名称进行连接，请尝试使用 IP 和端口地址（例如）。 `123.45.678.9:4022` 4024 是 Visual Studio 2019 x64 远程调试器的默认端口。 有关其他远程调试器端口分配，请参阅[远程调试器端口分配](remote-debugger-port-assignments.md)。

     ::: moniker-end
     ::: moniker range="vs-2017"

     > [!NOTE]
     > 如果无法使用远程计算机名称进行连接，请尝试使用 IP 和端口地址（例如）。 `123.45.678.9:4022` 4022 是 Visual Studio 2017 x64 远程调试器的默认端口。 有关其他远程调试器端口分配，请参阅[远程调试器端口分配](remote-debugger-port-assignments.md)。

     ::: moniker-end

   - 选择 **"连接目标**"框旁边的 **"查找**"按钮以打开 **"远程连接**"对话框。 "**远程连接"** 对话框列出了本地子网上或直接连接到计算机的所有设备。 您可能需要在服务器上[打开 UDP 端口 3702](../debugger/remote-debugger-port-assignments.md)才能发现远程设备。 选择所需的计算机或设备，然后单击"**选择**"。

   > [!NOTE]
   > “连接类型”设置在调试会话之间保持不变。而“连接目标”设置只有在成功与该目标建立了调试连接时才会在调试会话之间保持不变。

3. 单击“刷新”，填充“可用进程”列表********。

    >[!TIP]
    >“附加到进程”对话框处于打开状态时，进程可以在后台启动和停止，因此正在运行的进程列表可能不总是最新内容****。 可随时选择“刷新”查看当前列表****。

4. 在“可用进程”列表中，查找并选择要附加到的一个或多个进程****。

   - 若要快速选择一个进程，请在“筛选进程”框中键入其名称或首字母****。

   - 如果不知道进程名称，请浏览列表或参阅[常见调试方案](#BKMK_Scenarios)，了解一些常见的进程名称。

   - 若要查找所有用户帐户下运行的进程，请选择“显示所有用户的进程”复选框****。

     >[!NOTE]
     >如果尝试附加到不受信任的用户帐户拥有的进程，则会出现安全警告对话框确认。 有关详细信息请参阅[安全警告：附加到不受信任的用户所拥有的进程可能很危险。如果以下信息看上去可疑或者你无法确定，请勿附加到此进程](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user.md).

5. 在“附加到”字段中，确保已列出计划调试的代码类型****。 默认的“自动”设置适用于大多数应用类型****。

   要手动选择代码类型：
   1. 单击“选择”  。
   1. 在“选择代码类型”对话框中，选择“调试这些代码类型”********。
   1. 选择要调试的代码类型。
   1. 选择“确定”  。

6. 选择“附加”。****

>[!NOTE]
>可附加到多个应用进行调试，但在调试器中一次只能有一个应用处于活动状态。 可在 Visual Studio 的“调试位置”工具栏或“进程”窗口中设置活动的应用********。

在某些情况下，在远程桌面（终端服务）会话中进行调试时，“可用进程”列表时不会显示所有可用进程****。 如果以受限制的用户帐户的用户身份运行 Visual Studio，则“可用进程”列表不会显示在会话 0 中运行的进程****。 会话 0 用于服务和其他服务器进程，包括 w3wp.exe**。 你可以通过以下方法解决该问题：使用管理员帐户运行 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 或从服务器控制台而不是“终端服务”会话运行 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

如果这两种解决方法都不奏效，第三种方法是通过从 Windows 命令行运行 `vsjitdebugger.exe -p <ProcessId>` 来附加到进程。 您可以使用*tlist.exe*确定进程 ID。 要获取*tlist.exe，* 请下载并安装 Windows 的调试工具，可在[WDK 和 WinDbg 下载中](/windows-hardware/drivers/download-the-wdk)使用。

::: moniker range=">= vs-2019"


## <a name="attach-to-a-net-core-process-running-on-linux-using-ssh"></a>使用 SSH 连接到在 Linux 上运行的 .NET 核心进程

有关详细信息，请参阅使用[SSH 在 Linux 上运行的远程调试 .NET 内核](../debugger/remote-debugging-dotnet-core-linux-with-ssh.md)。

## <a name="attach-to-a-process-running-on-a-linux-docker-container"></a><a name="BKMK_Linux_Docker_Attach"></a>附加到在 Linux Docker 容器上运行的进程

您可以使用 **"附加到进程"** 对话框将 Visual Studio 调试器附加到本地或远程计算机上的 Linux .NET Core Docker 容器中运行的进程。

> [!IMPORTANT]
> 要使用此功能，必须安装 .NET 核心跨平台开发工作负荷，并具有对源代码的本地访问权限。

**要附加到 Linux Docker 容器中的正在运行的进程，请：**

1. 在可视化工作室中，选择**调试>附加到进程 （CTRL_ALT_P）** 以打开 **"附加到进程**"对话框。

![附加到进程菜单](../debugger/media/attach-process-menu.png "Attach_To_Process_Menu")

2. 将**连接类型**设置为**Docker（Linux 容器）。**
3. 选择 **"查找..."** 可通过 **"选择 Docker 容器"** 对话框设置**连接目标**。

    您可以在本地或远程调试 Docker 容器进程。
    
    **要在本地调试 Docker 容器进程，**
    1. 将**Docker CLI 主机**设置为**本地计算机**。
    1. 选择要从列表中附加到的正在运行的容器，然后按 **"确定**"。
    
    ![选择 Docker 容器菜单](../debugger/media/select-docker-container.png "Select_Docker_Container_Menu")
 
    **B. 要远程调试 Docker 容器进程：**
    
    > [!NOTE] 
    > 有两个选项用于远程连接到 Docker 容器中的正在运行的进程。 如果本地计算机上未安装 Docker 工具，则使用 SSH 的第一个选项是理想的选择。  如果确实在本地安装了 Docker 工具，并且具有配置为接受远程请求的 Docker 守护进程，请使用 Docker 守护进程尝试第二个选项。

    1. ***要通过 SSH 连接到远程计算机：***
        1. 选择 **"添加..."** 以连接到远程系统。<br/>
        ![连接到远程系统](../debugger/media/connect-remote-system.png "连接到远程系统")
        1. 选择一个正在运行的容器，在成功连接到 SSH 或守护进程并命中 **"确定"** 后附加到该容器。

    
    1. ***将目标设置为通过[Docker 守护进程](https://docs.docker.com/engine/reference/commandline/dockerd/)运行进程的远程容器***
        1. 在**Docker 主机（可选）** 下指定守护进程地址（即通过 TCP、IP 等），然后单击刷新链接。
        1. 选择一个正在运行的容器，在成功连接到守护进程并命中 **"确定**"后附加到该容器。

4. 从**可用进程**列表中选择相应的容器进程，然后选择 **"附加"** 以在 Visual Studio 中开始调试 C# 容器进程！

    ![已完成的 Docker 附加菜单](../debugger/media/docker-attach-complete.png "已完成 Linux Docker 附加菜单")
    

## <a name="attach-to-a-process-running-on-a-windows-docker-container"></a><a name="BKMK_Windows_Docker_Attach"></a>附加到在 Windows Docker 容器上运行的进程

您可以使用"**附加到进程"** 对话框将 Visual Studio 调试器附加到本地计算机上的 Windows Docker 容器中运行的进程。

> [!IMPORTANT]
> 要将此功能与 .NET Core 进程一起使用，您必须安装 .NET 核心跨平台开发工作负荷，并具有对源代码的本地访问权限。

**要附加到 Windows Docker 容器中的正在运行的进程，请：**

1. 在可视化工作室中，选择**调试>附加到进程**（或**CTRL_ALT_P）** 以打开 **"附加到进程**"对话框。

   ![附加到进程菜单](../debugger/media/attach-process-menu-docker-windows.png "Attach_To_Process_Menu")

2. 将**连接类型**设置为**Docker（Windows 容器）。**
3. 选择 **"查找..."** 以使用 **"选择 Docker 容器"** 对话框设置**连接目标**。

    > [!IMPORTANT]
    > 目标进程必须具有与运行的 Docker Windows 容器相同的处理器体系结构。
    
   通过 SSH 将目标设置为远程容器当前不可用，并且只能使用 Docker 守护进程来完成。
    
    ***将目标设置为通过[Docker 守护进程](https://docs.docker.com/engine/reference/commandline/dockerd/)运行进程的远程容器***
    1. 在**Docker 主机（可选）** 下指定守护进程地址（即通过 TCP、IP 等），然后单击刷新链接。 

    1. 选择成功连接到守护进程后要附加到的正在运行的容器，然后选择"确定"。
    
4. 从**可用进程**列表中选择相应的容器进程，然后选择 **"附加"** 以开始调试 C# 容器进程。

    ![已完成的 Docker 附加菜单](../debugger/media/docker-attach-complete-windows.png "已完成 Windows Docker 附加菜单")
    

5.  从可用进程列表中选择相应的容器进程，然后选择 **"附加"** 以开始调试 C# 容器进程。


::: moniker-end

## <a name="reattach-to-a-process"></a><a name="BKMK_reattach"></a>重新附加到进程

通过选择**调试** > **重新附加到进程****（Shift**+**Alt**+**P），** 您可以快速重新附加到以前附加到的进程。 当选择此命令时，调试器会立即尝试附加到最后连接的进程，方法是首次尝试匹配先前的进程 ID ，如果失败，将匹配先前的进程名称。 如果不找到任何匹配项，或多个进程具有相同的名称，“附加到进程” 对话框将打开，这样您就可以选择正确的进程****。

> [!NOTE]
> "**重新附加到进程"** 命令可从 Visual Studio 2017 中开始。

## <a name="common-debugging-scenarios"></a><a name="BKMK_Scenarios"></a>常见的调试方案

为帮助确定是否使用“附加到进程”以及要附加到的进程，下表显示了一些常见调试方案，并提供了指向更多可用说明的链接****。 （该列表并未列出详尽信息。）

对于某些应用类型，如通用 Windows 应用 (UWP) ，不能直接附加到进程名称，而需使用 Visual Studio 中的“调试安装的应用程序包”菜单选项（请参阅表格）****。

为使调试器附加到用 C++ 编写的代码，该代码需要发出 `DebuggableAttribute`。 可通过链接 [/ASSEMBLYDEBUG](/cpp/build/reference/assemblydebug-add-debuggableattribute) 链接器选项将它自动添加到代码中。

对于客户端脚本调试，必须在浏览器中启用脚本调试。 要在 Chrome 上调试客户端脚本，请选择**JavaScript（Chrome）** 或**JavaScript（微软边缘 - 铬）** 作为代码类型，并且根据您的应用类型，您可能需要关闭所有 Chrome 实例并在调试模式下启动浏览器（从命令行键入`chrome.exe --remote-debugging-port=9222`）。 在早期版本的 Visual Studio 中，Chrome 的脚本调试器是**Web 工具包**。

要快速选择要附加到的视觉工作室中的正在运行的进程，请在"视觉工作室"中键入**Ctrl**+**Alt**+**P，** 然后键入进程名称的第一个字母。

|场景|调试方法|进程名称|备注和链接|
|-|-|-|-|
|iIS 服务器上的远程调试ASP.NET 4 或 4.5|使用远程工具并**附加到流程**|*w3wp.exe*|请参阅[远程 IIS 计算机上的远程调试ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)|
|IIS 服务器上的远程调试ASP.NET核心|使用远程工具并**附加到流程**|*w3wp.exe*或*dotnet.exe*|从 .NET Core 3 开始 *，w3wp.exe*进程用于默认[的应用内托管模型](/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-3.1#hosting-models)。 有关应用部署，请参阅[发布到 IIS](/aspnet/core/host-and-deploy/iis/)。 有关详细信息，请参阅[远程 IIS 计算机上的远程调试ASP.NET酷睿](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md#BKMK_attach)|
|调试本地 IIS 服务器上的客户端脚本，用于受支持的应用类型 |使用**附加到流程**|*chrome.exe，**微软EdgeCP.exe，* 或*iexplore.exe*|必须启用脚本调试。 对于 Chrome，您还必须在调试模式下运行 Chrome（`chrome.exe --remote-debugging-port=9222`从命令行键入），并在 **"附加到**"字段中选择**JavaScript（Chrome）。**|
|在本地计算机上调试 C#、可视基础或C++应用|使用标准调试 （**F5**） 或**附加到进程**|*\<应用程序名称>.exe*|在大多数情况下，使用标准调试而不是**附加到进程**。|
|远程调试 Windows 桌面应用|远程工具|空值| 请参阅[远程调试 C# 或可视化基本应用](../debugger/remote-debugging-csharp.md)或[远程调试C++应用](../debugger/remote-debugging-cpp.md)|
|调试 .NET Linux 上的内核|使用**附加到流程**|*dotnet.exe*|要使用 SSH，请参阅[使用 SSH 在 Linux 上运行的远程调试 .NET 内核](../debugger/remote-debugging-dotnet-core-linux-with-ssh.md)。 |
|在没有调试器的情况下启动应用后，在本地计算机上调试ASP.NET应用|使用**附加到流程**|*iiexpress.exe*|这可能有助于使应用加载速度更快，例如（例如）分析时。 |
|在服务器进程中调试其他受支持的应用类型|如果服务器是远程的，请使用远程工具并**附加到进程**|*铬.exe，* *iexplore.exe，* 或其他过程|如有必要，请使用资源监视器来帮助标识该过程。 请参阅[远程调试](../debugger/remote-debugging.md)。|
|远程调试通用 Windows 应用 （UWP）、OneCore、HoloLens 或 IoT 应用|调试安装的应用包|空值|请参阅[调试已安装的应用包](debug-installed-app-package.md)，而不是使用**附加到进程**|
|调试通用 Windows 应用 （UWP）、OneCore、HoloLens 或 IoT 应用，而这些应用不是从可视化工作室启动的|调试安装的应用包|空值|请参阅[调试已安装的应用包](debug-installed-app-package.md)，而不是使用**附加到进程**|

## <a name="use-debugger-features"></a>使用调试器功能

要在附加到进程时使用 Visual Studio 调试器的全部功能（如命中断点），应用必须完全匹配本地源和符号。 也就是说，调试器必须能够加载正确的[符号 （.pdb） 文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。 默认情况下，这需要调试生成。

对于远程调试方案，必须已在 Visual Studio 中打开了源代码（或源代码的副本）。 远程计算机上编译的应用二进制文件必须与本地计算机上的源自同一版本。

在某些本地调试方案中，如果应用中存在正确的符号文件，则可以在 Visual Studio 中进行调试而无法访问源。 默认情况下，这需要调试生成。 有关详细信息，请参阅[指定符号和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。

## <a name="troubleshoot-attach-errors"></a><a name="BKMK_Troubleshoot_attach_errors"></a>排除附加错误
 当调试器附加到一个正在运行的进程时，该进程可能包含一种或多种类型的代码。 可在 **“选择代码类型”** 对话框中显示并选择可将调试器附加到的代码类型。

 有时，调试器能够成功附加到一种代码类型，但不能附加到另一种代码类型。 这种情况可能发生在你尝试附加到远程计算机上运行的进程时。 原因是远程计算机上可能安装了一些代码类型的远程调试组件，但没有安装另一些代码类型的远程调试组件。 这种情况还可能发生在你尝试为直接数据库调试附加到两个或多个进程时。 SQL 调试仅支持附加到单个进程。

 如果调试器能够附加到某些（但不是全部）代码类型，则会看到一条消息，标识哪些类型未附加。

 如果调试器成功地附加到至少一种代码类型，你就可以继续调试进程。 你只能调试那些已被成功附加的代码类型。 进程中的未附加代码仍将运行，但您将无法设置断点、查看数据或对该代码执行其他调试操作。

 如果想要有关调试器未能附加到代码类型的更具体信息，请尝试仅重新附加到该代码类型。

 **要获取有关代码类型未附加的原因的特定信息，请：**

1. 从进程中分离。 在**调试**菜单上，选择 **"全部分离**"。

1. 重新附加到进程，仅选择未附加的代码类型。

    1. 在"**附加到进程"** 对话框中，在 **"可用进程**"列表中选择该进程。

    2. 选择“选择”****。

    3. 在 **“选择代码类型”** 对话框中，选择 **“调试以下代码类型”** 和未能附加的代码类型。 取消选择其他代码类型。

    4. 选择“确定”  。

    5. 在"**附加到进程"** 对话框中，选择 **"附加**"。

    此时，附加将彻底失败，并且你将收到一条特定的错误消息。

## <a name="see-also"></a>另请参阅

- [调试多个进程](../debugger/debug-multiple-processes.md)
- [及时调试](../debugger/just-in-time-debugging-in-visual-studio.md)
- [远程调试](../debugger/remote-debugging.md)
