---
title: 错误:“Microsoft Visual Studio 远程调试监视器”(MSVSMON.EXE) 似乎没有在远程计算机上运行。
titleSuffix: ''
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.server_machine_no_default
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9a2c35befa92e72e08fe2e058afe10d19ac116e0
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73188138"
---
# <a name="error-the-microsoft-visual-studio-remote-debugging-monitor-msvsmonexe-does-not-appear-to-be-running-on-the-remote-computer"></a>错误:“Microsoft Visual Studio 远程调试监视器”(MSVSMON.EXE) 似乎没有在远程计算机上运行。
此错误消息表示 Visual Studio 未能在远程计算机上找到 Visual Studio 远程调试监视器的正确实例。 必须安装 Visual Studio 远程调试监视器以便进行远程调试。 有关下载和设置远程调试器的信息，请参阅[远程调试](../debugger/remote-debugging.md)。

> [!IMPORTANT]
> 如果你认为你因产品 bug 而收到此消息，请[向 Visual Studio 报告此问题](../ide/how-to-report-a-problem-with-visual-studio.md)。 如果需要更多帮助，请参阅 [Talk to Us](../ide/feedback-options.md) 了解与 Microsoft 联系的方法。

## <a name="i-got-this-message-while-i-was-debugging-in-visual-studio-2010-or-earlier"></a>我在 Visual Studio 2010 或更早版本中进行调试时收到了此消息
 当你使用的 Visual Studio 是 Visual Studio 2010 或更早版本时，如果文件和打印机共享未启用，则也可能收到此错误。 若要了解有关此问题的详细信息，请参阅本文档的 Visual Studio 2010 版本：[错误：Microsoft Visual Studio 远程调试监视器 (MSVSMON.EXE) 似乎没有在远程计算机上运行。- Visual Studio 2010](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms164726(v=vs.100))

## <a name="i-got-this-message-while-i-was-debugging-locally"></a>我在本地调试时收到了此消息
 如果在本地调试时收到此消息，问题可能出在你的防病毒软件或第三方防火墙。 Visual Studio 是一个 32 位应用程序，因此它使用 64 位的远程调试器版本来调试 64 位应用程序。 两个进程使用本地计算机内的本地网络进行通信。 计算机会持续进行通信，但第三方安全软件可能会阻止通信。

 以下各节列出其他一些你可能收到此消息的原因，以及解决此问题的操作。

## <a name="the-remote-machine-is-not-reachable"></a>远程计算机不可访问
 尝试 [ping](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee624059(v=ws.10)) 远程计算机。 如果它不响应 ping 操作，则远程工具也将无法连接。 请尝试重新启动远程计算机，或者确保它在网络上正确配置。

## <a name="the-version-of-the-remote-debugger-doesnt-match-the-version-of-visual-studio"></a>远程调试器的版本不匹配 Visual Studio 的版本
 在本地运行的 Visual Studio 的版本必须与远程计算机上运行的远程调试监视器的版本匹配。 若要解决此问题，请下载并安装匹配的远程调试监视器版本。 转到 [下载中心](https://www.microsoft.com/download) 以查找正确版本的远程调试器。

## <a name="the-local-and-remote-machines-have-different-authentication-modes"></a>本地和远程计算机具有不同的身份验证模式
 本地和远程计算机需要使用相同的身份验证模式。 若要解决此问题，请确保这两台计算机使用相同的身份验证模式。 有关身份验证模式的详细信息，请参阅 [Windows 身份验证概述](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831472(v=ws.11))。

## <a name="the-remote-debugger-is-running-under-a-different-user-account"></a>远程调试器使用不同的用户帐户运行
 可通过下列方法之一解决此问题：

- 你可以停止远程调试器，并使用本地计算机上使用的帐户重新启动它。

- 可以使用“/allow \<username>”参数 `msvsmon /allow <username@computer>` 从命令行启动远程调试器

- 可以将此用户添加到远程调试器权限（在远程调试器窗口“工具”>“权限”）。

- 如果你不能使用前面步骤中的方法，可以允许任何用户进行远程调试。 在远程调试器窗口中，转到“工具”>“选项”对话框。 选中“无身份验证”后，可选中“允许任何用户进行调试”。 但仅当你别无选择或在专用网络上操作时才应使用此选项。

## <a name="the-firewall-on-the-remote-machine-doesnt-allow-incoming-connections-to-the-remote-debugger"></a>远程计算机上的防火墙不允许对远程调试器的传入连接
 Visual Studio 计算机上的防火墙和远程计算机上的防火墙都必须配置为允许在 Visual Studio 和远程调试器之间进行通信。 有关远程调试器使用的端口的信息，请参阅 [Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)。 有关配置 Windows 防火墙的信息，请参阅 [Configure the Windows Firewall for Remote Debugging](../debugger/configure-the-windows-firewall-for-remote-debugging.md)。

## <a name="anti-virus-software-is-blocking-the-connections"></a>防病毒软件正在阻止连接
 Windows 防病毒软件允许远程调试器连接，但某些第三方防病毒软件可能会阻止它们。 查看你防病毒软件的文档以了解如何允许这些连接。

## <a name="network-security-policy-is-blocking-communication-between-the-remote-machine-and-visual-studio"></a>网络安全策略阻塞远程计算机和 Visual Studio 之间的通信
 查看网络安全以确保它没有阻止通信。 有关 Windows 网络安全策略的详细信息，请参阅[安全策略设置](/windows/device-security/security-policy-settings/security-policy-settings)。

## <a name="the-network-is-too-busy-to-support-remote-debugging"></a>网络太忙无法支持远程调试
 你可能需要在另一个时间进行远程调试，或重新安排另一个时间进行网络上的工作。

## <a name="more-help"></a>更多帮助
 若要获取更多远程调试器的帮助（包括命令行开关），请在远程调试器窗口中单击 "**帮助" > 用法**"。 如果尚未打开，可以通过将以下行复制到 "**文件资源管理器**" 窗口来查看网页。 （需要将 \<Visual Studio 安装目录 > 替换为 Visual Studio 安装的位置。）

 res:// *\<Visual Studio 安装目录 >* \ COMMON7 \ IDE \ 远程 %2 0 调试器 \ x64 \ msvsmon .exe/help .htm

## <a name="see-also"></a>请参阅
- [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)
