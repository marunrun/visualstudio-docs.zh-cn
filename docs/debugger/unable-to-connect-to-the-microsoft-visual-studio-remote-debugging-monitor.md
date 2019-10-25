---
title: 无法连接到 Microsoft Visual Studio 远程调试监视器 |Microsoft Docs
ms.date: 08/24/2017
ms.topic: reference
f1_keywords:
- vs.debug.error.remote_debug
- vs.debug.error.firewall.remotemachine
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
ms.openlocfilehash: 872f7c594344af2c59ebe7f8d1fbd1a640dd2190
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72728824"
---
# <a name="unable-to-connect-to-the-microsoft-visual-studio-remote-debugging-monitor"></a>Unable to Connect to the Microsoft Visual Studio Remote Debugging Monitor
出现此消息的原因可能是远程计算机上的远程调试监视器未正确设置，或者由于网络问题或存在防火墙而导致远程计算机无法访问。

> [!IMPORTANT]
> 如果你认为你因产品 bug 而收到此消息，请向 Visual Studio[报告此问题](../ide/how-to-report-a-problem-with-visual-studio.md)。 如果需要更多帮助，请参阅 [Talk to Us](../ide/talk-to-us.md) 了解与 Microsoft 联系的方法。

## <a name="specificerrors"></a>详细的错误消息是什么？

`Unable to Connect to the Microsoft Visual Studio Remote Debugging Monitor`是通用消息。 通常情况下，更具体的消息包含在错误字符串，也许能够帮助你确定问题或搜索更精确的修补程序的原因。 下面是几个附加到主错误消息的更常见的错误消息：

- [调试器无法连接到远程计算机。调试器无法解析指定的计算机名](#cannot_connect)
- [远程调试器拒绝了连接请求](#rejected)
- [对内存位置的访问无效](#invalid_access)
- [远程计算机上没有运行指定名称的服务器](#no_server)
- [请求的名称有效，但找不到请求类型的数据](#valid_name)
- [目标计算机上的 Visual Studio 远程调试器无法连接回此计算机](#cant_connect_back)
- [访问被拒绝](#access_denied)
- [发生了安全包特定的错误](#security_package)

## <a name="cannot_connect"></a>调试器无法连接到远程计算机。 调试器无法解析指定的计算机名

请尝试以下步骤：

1. 请确保在 "**附加到进程**" 对话框或项目属性中输入有效的计算机名和端口号（若要设置属性，请参阅[以下步骤](#server_incorrect)）。 计算机名称必须采用以下格式：

    `computername:port`

    > [!NOTE]
    > 端口号必须与必须在目标计算机上*运行*的[远程调试器的端口号](../debugger/remote-debugger-port-assignments.md)匹配。

2. 如果计算机名不起作用，请改为尝试 IP 地址和端口号。

3. 请确保在目标计算机上运行的远程调试器的版本与 Visual Studio 的版本匹配。 若要获取正确版本的远程调试器，请参阅[远程调试](../debugger/remote-debugging.md)。

    > [!TIP]
    > 如果要附加到进程并成功连接，但未看到所需的进程，请选中 "**显示所有用户的进程" 复选框**。 如果你使用不同的用户帐户进行连接，则将显示进程。

4. 如果这些步骤不能解决此错误，请参阅[远程计算机不可访问](#dns)。

## <a name="rejected"></a>远程调试器拒绝了连接请求

在 "**附加到进程**" 对话框或项目属性中，确保远程计算机名称和端口号与远程调试器窗口中显示的名称和端口号匹配。 如果不正确，请修复，然后重试。

如果这些值正确且消息提到**Windows 身份验证**模式，请检查远程调试器是否处于正确的身份验证模式（"**工具" > "选项**"）。

## <a name="invalid_access"></a>对内存位置的访问无效

发生内部错误。 重新启动 Visual Studio 并重试。

## <a name="no_server"></a>远程计算机上没有运行指定名称的服务器

Visual Studio 无法连接到远程调试器。 此消息可能由以下几个原因导致：

- 远程调试器可能在不同的用户帐户下运行。 请参阅[以下步骤](#user_accounts)

- 防火墙上的端口被阻止。 请确保防火墙[未阻止你的请求](#firewall)，尤其是在你使用第三方防火墙时。

- 远程调试器版本与 Visual Studio 不匹配。 若要获取正确版本的远程调试器，请参阅[远程调试](../debugger/remote-debugging.md)。

## <a name="valid_name"></a>请求的名称有效，但找不到请求类型的数据

远程计算机存在，但 Visual Studio 无法连接到远程调试器。 此消息可能由以下几个原因导致：

- DNS 问题正在阻止连接。 请参阅[以下步骤](#dns)。

- 远程调试器可能在不同的用户帐户下运行。 请执行[这些步骤](#user_accounts)。

- 防火墙上的端口被阻止。 请确保防火墙[未阻止你的请求](#firewall)，尤其是在你使用第三方防火墙时。

- 远程调试器版本与 Visual Studio 不匹配。 若要获取正确版本的远程调试器，请参阅[远程调试](../debugger/remote-debugging.md)。

## <a name="cant_connect_back"></a>目标计算机上的 Visual Studio 远程调试器无法连接回此计算机

远程调试器可能在不同的用户帐户下运行。 在远程调试器中，打开 "**工具" > 权限**，以将用户添加到远程调试器的权限。 有关详细信息，请参阅[远程调试器正在不同的用户帐户下运行](#user_accounts)。

如果错误消息也提到了防火墙，则本地计算机上的防火墙可能会阻止从远程计算机到 Visual Studio 的通信。 请参阅[以下步骤](#firewall)。

## <a name="access_denied"></a> 访问被拒绝

如果尝试从32位计算机上的64位远程计算机上进行调试，则可能会看到此错误。

## <a name="security_package"></a>发生了安全包特定的错误

这可能是特定于 Windows XP 和 Windows 7 的遗留问题。 请参阅此[信息](https://stackoverflow.com/questions/4786016/unable-to-connect-to-the-microsoft-remote-debugging-monitor-a-security-package)。

## <a name="causes-and-recommendations"></a>原因和建议

### <a name="dns"></a> 远程计算机不可访问

如果无法使用远程计算机名称进行连接，请尝试改用 IP 地址。 可以在远程计算机上的命令行中使用 `ipconfig` 来获取 IPv4 地址。 如果使用的是主机文件，请验证是否已正确配置。

如果失败，请验证是否可以在网络上访问远程计算机（对远程计算机执行[ping](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee624059(v=ws.10))操作）。 不支持通过 Internet 进行远程调试，在某些 Microsoft Azure 情况下除外。

### <a name="server_incorrect"></a>服务器名称不正确，或者第三方软件正在干扰远程调试器

在 Visual Studio 中查看项目属性，并确保服务器名称正确无误。 请参阅主题， [ C#并 Visual Basic](../debugger/remote-debugging-csharp.md#remote_csharp)和。 [C++](../debugger/remote-debugging-cpp.md#remote_cplusplus) 对于 ASP.NET，打开 "**属性/Web/服务器**" 或 "**属性"/"调试**"，具体取决于项目类型。

> [!NOTE]
> 如果要附加到进程，则不会使用项目属性中的远程设置。

如果服务器名称正确，则您的防病毒软件或第三方防火墙可能会阻止远程调试器。 在本地调试时，可能会发生这种情况，因为 Visual Studio 是一个32位应用程序，因此它使用64位版本的远程调试器来调试64位应用程序。 32位和64位进程使用本地计算机内的本地网络进行通信。 计算机会持续进行网络通信，但第三方安全软件可能会阻止通信。

### <a name="user_accounts"></a> 远程调试器使用不同的用户帐户运行

默认情况下，远程调试器只接受来自启动远程调试器和 Administrators 组成员的用户的连接。 必须向其他用户显式授予权限。

可通过下列方法之一解决此问题：

- 将 Visual Studio 用户添加到远程调试器权限（在远程调试器窗口中，选择 "**工具" > 权限**）。

- 在远程计算机上，使用在 Visual Studio 计算机上使用的同一用户帐户和密码重新启动远程调试器。

    > [!NOTE]
    > 如果在远程服务器上运行远程调试器，请右键单击远程调试器应用并选择 "**以管理员身份运行**" （或者，你可以将远程调试器作为服务运行）。 如果未在远程服务器上运行，只需正常启动。

- 可以使用“/allow \<username>”参数 `msvsmon /allow <username@computer>` 从命令行启动远程调试器。

- 或者，您可以允许任何用户进行远程调试。 在远程调试器窗口中，转到“工具”>“选项”对话框。 选中“无身份验证”后，可选中“允许任何用户进行调试”。 但是，只应在其他选项失败时或在专用网络上使用此选项。

### <a name="firewall"></a> 远程计算机上的防火墙不允许对远程调试器使用传入连接
 Visual Studio 计算机上的防火墙和远程计算机上的防火墙都必须配置为允许在 Visual Studio 和远程调试器之间进行通信。 有关远程调试器使用的端口的信息，请参阅 [Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)。 有关配置 Windows 防火墙的信息，请参阅 [Configure the Windows Firewall for Remote Debugging](../debugger/configure-the-windows-firewall-for-remote-debugging.md)。

### <a name="the-version-of-the-remote-debugger-doesnt-match-the-version-of-visual-studio"></a>远程调试器的版本不匹配 Visual Studio 的版本
 在本地运行的 Visual Studio 的版本必须与远程计算机上运行的远程调试监视器的版本匹配。 若要解决此问题，请下载并安装匹配的远程调试监视器版本。 若要获取正确版本的远程调试器，请参阅[远程调试](../debugger/remote-debugging.md)。

### <a name="the-local-and-remote-machines-have-different-authentication-modes"></a>本地和远程计算机具有不同的身份验证模式
 本地和远程计算机需要使用相同的身份验证模式。 若要解决此问题，请确保这两台计算机使用相同的身份验证模式。 可以更改身份验证模式。 在远程调试器窗口中，请切换到 "**工具" > 选项**"对话框。

 有关身份验证模式的详细信息，请参阅 [Windows 身份验证概述](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831472(v=ws.11))。

### <a name="anti-virus-software-is-blocking-the-connections"></a>防病毒软件正在阻止连接
 Windows 防病毒软件允许远程调试器连接，但某些第三方防病毒软件可能会阻止它们。 查看你防病毒软件的文档以了解如何允许这些连接。

### <a name="network-security-policy-is-blocking-communication-between-the-remote-machine-and-visual-studio"></a>网络安全策略阻塞远程计算机和 Visual Studio 之间的通信
 查看网络安全以确保它没有阻止通信。 有关 Windows 网络安全策略的详细信息，请参阅[安全策略设置](/windows/device-security/security-policy-settings/security-policy-settings)。

### <a name="the-network-is-too-busy-to-support-remote-debugging"></a>网络太忙无法支持远程调试
 你可能需要在另一个时间进行远程调试，或重新安排另一个时间进行网络上的工作。

## <a name="more-help"></a>更多帮助
 若要获取更多远程调试器帮助，请打开远程调试器的 "帮助" 页（帮助 > 远程调试器中的**使用情况**）。

## <a name="see-also"></a>请参阅
- [Remote Debugging](../debugger/remote-debugging.md)
