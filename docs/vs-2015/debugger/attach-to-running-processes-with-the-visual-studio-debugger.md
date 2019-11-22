---
title: Attach to Running Processes with the Debugger | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
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
- C++
- CSharp
- FSharp
- VB
- c++
helpviewer_keywords:
- remote debugging, attaching to programs
- processes, attaching to running processes
- Attach to Process dialog box
- debugging [Visual Studio], attaching to processes
- debugger, processes
ms.assetid: 27900e58-090c-4211-a309-b3e1496d5824
caps.latest.revision: 62
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 03cd890802e5563ce2daeb78438c56f4452d74f0
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299515"
---
# <a name="attach-to-running-processes-with-the-visual-studio-debugger"></a>使用 Visual Studio 调试器附加到运行的进程
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可将 Visual Studio 调试器附加到本地或远程计算机上正在运行的进程。 After the process is running, click **Debug / Attach to Process** (or press **CTRL+ALT+P**) to open the **Attach to Process** dialog box.

You can use this capability to debug apps that are running on a local or remote computer, debug multiple processes simultaneously, or debug an application that was not created in Visual Studio. It is often useful when you want to debug an app, but (for whatever reason) you did not start the app from Visual Studio with the debugger attached. For example, if you are running the app without the debugger and hit an exception, you might then attach to the process running the app to begin debugging.

> [!TIP]
> Not sure whether you need to use **Attach to Process** for your debugging scenario? 请参阅[常见调试方案](#BKMK_Scenarios)。 If you want to debug ASP.NET applications that have been deployed to IIS, see [Remote Debugging ASP.NET on a remote IIS computer](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md).

## <a name="BKMK_Attach_to_a_running_process"></a> Attach to a running process on the local machine
 In order to attach to a process, you must know the name of the process (see [Common debugging scenarios](#BKMK_Scenarios) for a few common process names).

1. In Visual Studio, select **Debug / Attach to Process** (or press **CTRL+ALT+P**).

2. 在 **“附加到进程”** 对话框中的 **“可用进程”** 列表中，找到要附加到的程序。

     To quickly select the process you want, type the first letter of the process name. If you don't know the process name, see [Common debugging scenarios](#BKMK_Scenarios).

     ![DBG_Basics_Attach_To_Process](../debugger/media/dbg-basics-attach-to-process.png "DBG_Basics_Attach_To_Process")

     如果进程在不同的用户帐户下运行，请选中“显示所有用户的进程”复选框。

3. 在“附加到” 对话框中，确保待调试的代码类型已经列出。 默认的 **“自动”** 设置尝试确定要调试的代码类型。 若要手动设置代码类型，请执行以下操作

    1. 在“附加到进程” 对话框中，单击“选择”。

    2. 在 **“选择代码类型”** 对话框中，单击 **“调试以下代码类型”** ，然后选择要调试的类型。

    3. 单击“确定”。

4. 单击 **“附加”** 。

## <a name="BKMK_Attach_to_a_process_on_a_remote_computer"></a>附加到远程计算机上的进程
 In order to attach to a process, you must know the name of the process (see [Common debugging scenarios](#BKMK_Scenarios) for a few common process names). For more complete guidance for ASP.NET apps that have been deployed to IIS, see [Remote Debugging ASP.NET on a remote IIS computer](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md). 对于其他应用，或许能够在任务管理器中找到进程的名称。

 当使用 **“附加到进程”** 对话框时，你可以选择另一台已经针对远程调试进行设置的计算机。 有关详细信息，请参阅[远程调试](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)。 选择了一台远程计算机后，可以查看该计算机上运行的可用进程的列表，并附加到一个或多个进程以进行调试。

 **To select a remote computer:**

1. In Visual Studio, select **Debug / Attach to Process** (or press **CTRL+ALT+P**).

2. 在 **“附加到进程”** 对话框中，从 **“传输”** 列表中选择适当的连接类型。 对于大部分程序来说， **“默认”** 是正确的设置。

   **“传输”** 设置在调试会话之间保持。

3. 使用“限定符” 列表框来通过以下方法之一选择远程计算机名称：

   1. 在 **“限定符”** 列表框中键入名称。

      > [!NOTE]
      > If, in later steps, you can't connect using the remote computer name, use the IP address. (The port number may appear automatically after selecting the process. You can also enter it manually. In the illustration below, 4020 is the default port for the remote debugger.)

   2. 单击附加到 **“限定符”** 列表框的下拉箭头，然后从下拉列表中选择计算机名称。

   3. Click the **Find** button next to the **Qualifier** list to open the **Select Remote Debugger Connection** dialog box. **“选择远程调试器连接”** 对话框将列出本地子网上的所有设备和通过以太网电缆直接连接到你的计算机的任何设备。 单击所需的计算机或设备，然后单击 **“选择”** 。

      **“限定符”** 设置只有相应的限定符发生了成功的调试连接时才会在调试会话之间保持。

4. 单击“刷新”。

     打开“进程”对话框时，“可用进程”列表自动显示。 该对话框处于打开状态时，进程可以在后台启动和停止。 不过，内容并非总是最新的。 通过单击 **“刷新”** ，可以随时刷新列表以查看当前进程列表。

5. 在 **“附加到进程”** 对话框中的 **“可用进程”** 列表中，找到要附加到的程序。

    如果进程在不同的用户帐户下运行，请选中“显示所有用户的进程”复选框。

6. 单击 **“附加”** 。

## <a name="additional-info"></a>Additional info

调试时可以附加到多个程序，但在任何时间，调试器中都只有一个程序处于活动状态。 可以在 **“调试位置”** 工具栏或 **“进程”** 窗口中设置活动程序。 有关详细信息，请参阅 [如何：设置当前程序](https://msdn.microsoft.com/7e1d7fa5-0e40-44cf-8c41-d3dba31c969e)。

如果尝试附加到不受信任的用户帐户拥有的进程，则会出现安全警告对话框确认。 有关详细信息请参阅[安全警告：附加到不受信任的用户所拥有的进程可能很危险。如果以下信息看上去可疑或者你无法确定，请勿附加到此进程](/visualstudio/debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user?view=vs-2015).

在某些情况下，在“远程桌面”（“终端服务”）会话中进行调试时， **“可用进程”** 列表不会显示所有可用进程。 如果以具有有限用户帐户的用户身份运行 Visual Studio，“可用进程” 列表将不显示在会话 0 中运行的进程，会话 0 用于服务与其他服务器进程，包括 w3wp.exe。 可通过以下方法解决该问题：使用管理员帐户运行 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 或从服务器控制台（而不是“终端服务”会话）运行 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 如果这两种解决方法都不奏效，第三种方法是通过从 Windows 命令行运行 `vsjitdebugger.exe -p` *ProcessId* 来附加到进程。 你可以使用 tlist.exe 来确定进程 ID。 若要获取 tlist.exe，可从  [WDK 和 WinDbg 下载](https://go.microsoft.com/fwlink/?LinkId=168279)中下载并安装 Windows 调试工具。

## <a name="BKMK_Scenarios"></a> Common debugging scenarios

To help you identify whether you need to use **Attach to process** and what process to attach to, a few common debugging scenarios are shown here (the list is not exhaustive). Where more instructions are available, we provide links.

For some app types (like Windows Store apps), you don't attach directly to a process name, but use the **Debug Installed App Package** menu option instead (see table).

> [!NOTE]
> For information about basic debugging in Visual Studio, see [Getting started with the debugger](../debugger/getting-started-with-the-debugger.md).

|方案|Debug Method|进程名|Notes and Links|
|-|-|-|-|
|Debug a managed or native app on the local machine|Use attach to process or [standard debugging](../debugger/getting-started-with-the-debugger.md)|*appname*.exe|To quickly access the dialog box, use **CTRL+ALT+P** and then type the first letter of the process name.|
|Debug ASP.NET apps on the local machine after starting the app without the debugger|Use attach to process|iiexpress.exe|This may be helpful to make your app load faster, such as (for example) when profiling. |
|Remote debug ASP.NET 4 or 4.5 on an IIS server|Use remote tools and attach to process|w3wp.exe|See [Remote Debugging ASP.NET on a remote IIS computer](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)|
|Remote debug ASP.NET Core on an IIS server|Use remote tools and attach to process|dnx.exe|For app deployment, see [Publish to IIS](https://docs.asp.net/en/latest/publishing/iis.html). For debugging, see [Remote Debugging ASP.NET on a remote IIS computer](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)|
|Debug other supported app types on a server process|Use remote tools (if server is remote) and attach to process|iexplore.exe or other processes|If necessary, use Task Manager to help identify the process. See [Remote Debugging](../debugger/remote-debugging.md) and later sections in this topic|
|Remote debug a Windows desktop app|Remote Tools and F5|不可用| See [Remote Debugging](../debugger/remote-debugging.md)|
|Remote debug a Windows Universal (UWP), OneCore, HoloLens, or IoT app|调试安装的应用包|不可用|Use **Debug / Other Debug Targets / Debug Installed App Package** instead of **Attach to process**|
|Debug a Windows Universal (UWP), OneCore, HoloLens, or IoT app that you didn't start from Visual Studio|调试安装的应用包|不可用|Use **Debug / Other Debug Targets / Debug Installed App Package** instead of **Attach to process**|

> [!WARNING]
> 若要附加到用 JavaScript 编写的 Windows 通用应用，必须先为该应用启用调试。 请参阅 Windows 开发人员中心中的 [Attach the debugger](../debugger/start-a-debugging-session-for-store-apps-in-visual-studio-javascript.md#BKMK_Attach_the_debugger) 。

> [!NOTE]
> 为使调试器附加到用 C++ 编写的代码，该代码需要发出 `DebuggableAttribute`。 可通过链接 [/ASSEMBLYDEBUG](https://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982) 链接器选项将它自动添加到代码中。

## <a name="what-debugger-features-can-i-use"></a>What debugger features can I use?

To use the full features of the Visual Studio debugger (like hitting breakpoints) when attaching to a process, the executable must exactly match your local source and symbols (that is, the debugger must be able to load the correct [symbol (.pbd) files](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)). By default, this requires a debug build.

对于远程调试方案，必须已在 Visual Studio 中打开了源代码（或源代码的副本）。 远程计算机上编译的应用二进制文件必须与本地计算机上的源自同一版本。

In some local debugging scenarios, you can debug in Visual Studio with no access to the source if the correct symbol files are present with the app (by default, this requires a debug build). For more info, see [Specify Symbol and Source Files](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

## <a name="BKMK_Troubleshoot_attach_errors"></a>排查附加错误
 当调试器附加到一个正在运行的进程时，该进程可能包含一种或多种类型的代码。 可在 **“选择代码类型”** 对话框中显示并选择可将调试器附加到的代码类型。

 有时，调试器能够成功附加到一种代码类型，但不能附加到另一种代码类型。 这种情况可能发生在你尝试附加到远程计算机上运行的进程时。 原因是远程计算机上可能安装了一些代码类型的远程调试组件，但没有安装另一些代码类型的远程调试组件。 这种情况还可能发生在你尝试为直接数据库调试附加到两个或多个进程时。 SQL 调试仅支持附加到单个进程。

 如果调试器能够附加到某些代码类型而不是所有代码类型，你将看到一条消息，指示无法附加的类型。

 如果调试器成功地附加到至少一种代码类型，你就可以继续调试进程。 你只能调试那些已被成功附加的代码类型。 上面的示例消息说明未能附加脚本代码类型。 因此，你将不能调试进程内的脚本代码。 进程内的脚本代码将继续运行，但无法设置断点、查看数据或在脚本中执行其他调试操作。

 如果想了解有关调试器未能附加到某种代码类型的详细原因，可以尝试仅重新附加到该代码类型。

 **To obtain specific information about why a code type failed to attach**

1. 从进程中分离。 在 **“调试”** 菜单上，单击 **“全部分离”** 。

2. 再次附加到进程，仅选择单一代码类型。

   1. 在 **“附加到进程”** 对话框的 **“可用进程”** 列表中选择进程。

   2. 单击 **“选择”** 。

   3. 在 **“选择代码类型”** 对话框中，选择 **“调试以下代码类型”** 和未能附加的代码类型。 清除任何其他代码。

   4. 单击“确定”。 **“选择代码类型”** 对话框关闭。

   5. 在 **“附加到进程”** 对话框中，单击 **“附加”** 。

      此时，附加将彻底失败，并且你将收到一条特定的错误消息。

## <a name="see-also"></a>请参阅
 [Debug Multiple Processes](../debugger/debug-multiple-processes.md) [Just-In-Time Debugging](../debugger/just-in-time-debugging-in-visual-studio.md) [Remote Debugging](../debugger/remote-debugging.md)
