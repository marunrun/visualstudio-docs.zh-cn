---
title: 无法连接到 Microsoft Visual Studio 远程调试监视器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.error.remote_debug
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: a1d959fc-3817-491c-831b-e6b768a3877a
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d62e7ce1c419a9c53e40e1ecf2f71497d60d7a23
ms.sourcegitcommit: 374f5ec9a5fa18a6d4533fa2b797aa211f186755
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77477061"
---
# <a name="unable-to-connect-to-the-microsoft-visual-studio-remote-debugging-monitor"></a>Unable to Connect to the Microsoft Visual Studio Remote Debugging Monitor
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当你在“附加到进程”  对话框中输入无效的 Visual Studio 远程调试监视器名称时，会出现此错误消息。 远程调试监视器名称通常与尝试连接以进行远程调试的计算机的名称相同。 出现此消息的原因可能是网络上不存在该远程计算机，远程计算机上的远程调试监视器未正确设置，或者由于网络问题或存在防火墙而导致远程计算机不可访问。  
  
> [!IMPORTANT]
> 如果需要更多帮助，请参阅 [Talk to Us](../ide/talk-to-us.md) 了解与 Microsoft 联系的方法。  
  
## <a name="i-got-this-message-while-i-was-debugging-locally"></a>我在本地调试时收到了此消息  
 如果在本地调试时收到此消息，问题可能出在你的防病毒软件或第三方防火墙。 Visual Studio 是一个 32 位应用程序，因此它使用 64 位的远程调试器版本来调试 64 位应用程序。 两个进程使用本地计算机内的本地网络进行通信。 计算机会持续进行网络通信，但第三方安全软件可能会阻止通信。  
  
 以下各节列出其他一些你可能收到此消息的原因，以及解决此问题的操作。  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
- 确保远程计算机上已安装并且正在运行 Visual Studio 远程调试监视器。 有关远程调试器及其安装方法的信息，请参阅[远程调试](../debugger/remote-debugging.md)。  
  
- 在 Visual Studio 中查看项目属性（“项目”/“属性”/“调试”）。 确保“远程服务器名称”  正确。  
  
- 验证远程计算机在网络上是可访问的。  
  
## <a name="the-remote-machine-is-not-reachable"></a>远程计算机不可访问  
 尝试 [ping](https://technet.microsoft.com/library/ee624059\(v=ws.10\).aspx) 远程计算机。 如果它不响应 ping 操作，则远程工具也将无法连接。 请尝试重新启动远程计算机，或者确保它在网络上正确配置。  
  
## <a name="the-version-of-the-remote-debugger-doesnt-match-the-version-of-visual-studio"></a>远程调试器的版本不匹配 Visual Studio 的版本  
 在本地运行的 Visual Studio 的版本必须与远程计算机上运行的远程调试监视器的版本匹配。 若要解决此问题，请下载并安装匹配的远程调试监视器版本。 请参阅[Visual studio 订阅](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)，查找适用于你的 Visual studio 版本的远程调试器的正确版本。

## <a name="the-local-and-remote-machines-have-different-authentication-modes"></a>本地和远程计算机具有不同的身份验证模式  

 本地和远程计算机需要使用相同的身份验证模式。 若要解决此问题，请确保这两台计算机使用相同的身份验证模式。 你可在“工具”/“选项”  对话框中的远程调试器上更改身份验证模式。  
  
 有关身份验证模式的详细信息，请参阅 [Windows 身份验证概述](https://technet.microsoft.com/library/hh831472.aspx)。  
  
## <a name="the-remote-debugger-is-running-under-a-different-user-account"></a>远程调试器使用不同的用户帐户运行  
 可通过下列方法之一解决此问题：  
  
- 你可以停止远程调试器，并使用本地计算机上使用的帐户重新启动它。  
  
- 可以使用“/allow **username>”参数 \< 从命令行启动远程调试器**`msvsmon /allow <username@computer>`  
  
- 你可以将此用户添加到远程调试器权限（在远程调试器窗口“工具/权限” ）。  
  
- 如果你不能使用前面步骤中的方法，可以允许任何用户进行远程调试。 在远程调试器窗口中，转到“工具/选项”  对话框。 选中“无身份验证”   后，可选中 “允许任何用户进行调试”。 但仅当你别无选择或在专用网络上操作时才应使用此选项。  
  
## <a name="the-firewall-on-the-remote-machine-doesnt-allow-incoming-connections-to-the-remote-debugger"></a>远程计算机上的防火墙不允许对远程调试器的传入连接  
 Visual Studio 计算机上的防火墙和远程计算机上的防火墙都必须配置为允许在 Visual Studio 和远程调试器之间进行通信。 有关远程调试器使用的端口的信息，请参阅 [Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)。 有关配置 Windows 防火墙的信息，请参阅 [Configure the Windows Firewall for Remote Debugging](../debugger/configure-the-windows-firewall-for-remote-debugging.md)。  
  
## <a name="anti-virus-software-is-blocking-the-connections"></a>防病毒软件正在阻止连接  
 Windows 防病毒软件允许远程调试器连接，但某些第三方防病毒软件可能会阻止它们。 查看你防病毒软件的文档以了解如何允许这些连接。  
  
## <a name="network-security-policy-is-blocking-communication-between-the-remote-machine-and-visual-studio"></a>网络安全策略阻塞远程计算机和 Visual Studio 之间的通信  
 查看网络安全以确保它没有阻止通信。 有关 Windows 网络安全策略的详细信息，请参阅 [安全管理](https://msdn.microsoft.com/library/windows/desktop/ms721855\(v=vs.85\).aspx)。  
  
## <a name="the-network-is-too-busy-to-support-remote-debugging"></a>网络太忙无法支持远程调试  
 你可能需要在另一个时间进行远程调试，或重新安排另一个时间进行网络上的工作。  
  
## <a name="more-help"></a>更多帮助  
 若要获取更多远程调试器的帮助（包括命令行开关），请在浏览器中打开以下内容：  
  
 **res://C:\Program%20Files\Microsoft%20Visual%20Studio%2014.0\Common7\IDE\Remote%20Debugger\x64\msvsmon.exe/help.htm**  
  
## <a name="see-also"></a>另请参阅  
 [远程调试](../debugger/remote-debugging.md)
