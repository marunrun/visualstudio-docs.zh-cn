---
title: 如何：附加到脚本 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- script debugging, attaching to script
- script, attaching to
- processes, attaching to script
- remote debugging, attaching to script
ms.assetid: 82013e9a-ef53-4fd2-b451-a6891cdc6307
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 993d1b3b6b4db6b435064a873142f563a950f4db
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387859"
---
# <a name="how-to-attach-to-script"></a>如何：附加到脚本
本主题介绍如何手动将 Visual Studio 调试器附加到脚本文件进行调试。

### <a name="to-attach-to-a-running-process"></a>附加到正在运行的进程

1. 在“调试”菜单上，选择“附加到进程”。 （如果未打开任何项目，则在“工具”菜单上选择“附加到进程”。）

2. 在“附加到进程”对话框中，查看“可用进程”列表，找到要附加到的脚本进程。 可查看“类型”列以识别脚本进程。

   1. 如果要调试的进程正在另一台计算机上运行，则必须先选择该远程计算机。

   2. 如果进程在不同的用户帐户下运行，请选中“显示所有用户的进程”复选框。

   3. 如果是通过 **“远程桌面连接”** 连接，请选中 **“显示所有会话中的进程”** 复选框。

3. 单击要附加到的进程。

4. 在中**将附加到**框中，你应看到**脚本代码**或**自动：脚本代码**。 如果显示其他内容，请按照下列步骤操作：

   1. 单击“选择”。

   2. 在 “选择代码类型”对话框中，单击“调试这些代码类型”，然后选择“脚本”。

   3. 单击 **“确定”**。

5. 单击 **“附加”**。

    此时您可能会看到一个警告，通知您 Internet Explorer 中已禁用脚本调试。 如果发生这种情况，请参阅[警告：脚本调试已禁用](../debugger/warning-script-debugging-disabled.md)。

   打开“进程”对话框时，“可用进程”列表自动显示。 该对话框处于打开状态时，进程可以在后台启动和停止。 因此，其中内容可能并非总是最新的。 可按“刷新”按钮随时刷新列表以查看当前进程列表。

   调试时可以附加到多个程序，但在任何时间，调试器中都只有一个程序处于活动状态。 可以在“调试位置”工具栏中设置活动程序。 有关详细信息，请参阅[如何：设置当前进程](/previous-versions/visualstudio/visual-studio-2010/d5d4sxdw(v=vs.100))。

   所有“调试”菜单执行命令都会影响活动程序。 可从“进程”对话框中断任何已调试的程序。请参阅[使用断点](../debugger/using-breakpoints.md)。

> [!NOTE]
> 如果尝试附加到不受信任的用户帐户拥有的进程，则会出现安全警告对话框确认。 有关详细信息，请参阅[安全警告：附加到不受信任的用户所拥有的进程可能很危险。以下信息看上去可疑或者你不确定，如果未附加到此进程](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user.md)。

 在某些情况下，在“终端服务”（“远程桌面”）会话中进行调试时，“可用进程”列表不会显示所有可用进程。 在 [!INCLUDE[WinXPSvr](../debugger/includes/winxpsvr_md.md)]或更高版本上，如果以受限用户的身份运行 Visual Studio，“可用进程”列表不会显示会话 0 中运行的进程，该会话用于服务和其他服务器进程（包括 w3wp.exe）。 可通过以下方法解决该问题：使用管理员帐户运行 Visual Studio，或从服务器控制台而非“终端服务”会话运行 Visual Studio。 如果这两种解决方法都不可行，第三种选择是通过在 Windows 命令行键入 vsjitdebugger.exe -p ProcessId 以附加到进程。 可使用 tlist.exe 来确定进程 ID。 若亚获取 tlist.exe，请下载并安装 Windows 调试工具，该工具可在 [Windows 硬件开发中心获得](/windows-hardware/drivers/dashboard/)。

## <a name="see-also"></a>请参阅
- [客户端脚本调试](../debugger/client-side-script-debugging.md)
- [附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [安全警告：附加到不受信任的用户所拥有的进程可能很危险。如果以下信息看上去可疑或者你无法确定，请勿附加到此进程](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user.md)
- [调试器安全](../debugger/debugger-security.md)