---
title: 无法连接到 Microsoft 可视化工作室远程调试监视器 |微软文档
ms.date: 04/14/2020
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
ms.openlocfilehash: d509292bc3c7a909289abf0c73babccfead31532
ms.sourcegitcommit: cc58ca7ceae783b972ca25af69f17c9f92a29fc2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "81385399"
---
# <a name="unable-to-connect-to-the-microsoft-visual-studio-remote-debugging-monitor"></a>Unable to Connect to the Microsoft Visual Studio Remote Debugging Monitor
由于远程调试监视器未在远程计算机上正确设置，或者由于网络问题或存在防火墙，无法访问远程计算机，因此可能会出现此消息。

> [!IMPORTANT]
> 如果您认为您因为产品错误而收到此消息，请向 Visual Studio[报告此问题](../ide/how-to-report-a-problem-with-visual-studio.md)。 如果需要更多帮助，请参阅 [Talk to Us](../ide/feedback-options.md) 了解与 Microsoft 联系的方法。

## <a name="what-is-the-detailed-error-message"></a><a name="specificerrors"></a>什么是详细的错误消息？

`Unable to Connect to the Microsoft Visual Studio Remote Debugging Monitor`是通用消息。 通常情况下，更具体的消息包含在错误字符串，也许能够帮助你确定问题或搜索更精确的修补程序的原因。 下面是几个附加到主错误消息的更常见的错误消息：

- [调试器无法连接到远程计算机。调试器无法解析指定的计算机名称](#cannot_connect)
- [远程调试器拒绝了连接请求](#rejected)
- [对内存位置的无效访问](#invalid_access)
- [远程计算机上没有按指定名称运行的服务器](#no_server)
- [请求的名称有效，但未找到请求类型的数据](#valid_name)
- [目标计算机上的可视化工作室远程调试器无法连接到此计算机](#cant_connect_back)
- [访问被拒绝](#access_denied)
- [发生安全包特定错误](#security_package)

## <a name="the-debugger-cannot-connect-to-the-remote-computer-the-debugger-was-unable-to-resolve-the-specified-computer-name"></a><a name="cannot_connect"></a>调试器无法连接到远程计算机。 调试器无法解析指定的计算机名称

请尝试以下步骤：

1. 请确保在 **"附加到流程**"对话框或项目属性（要设置属性）中输入有效的计算机名称和端口号（要设置属性，请参阅[这些步骤](#server_incorrect)）。 计算机名称必须具有以下格式：

    `computername:port`

    > [!NOTE]
    > 端口号必须与[远程调试器的端口号](../debugger/remote-debugger-port-assignments.md)匹配，远程调试器*必须在*目标计算机上运行。

2. 如果计算机名称不起作用，请尝试使用 IP 地址和端口号。

3. 确保在目标计算机上运行的远程调试器版本与您的 Visual Studio 版本匹配。 要获取远程调试器的正确版本，请参阅[远程调试](../debugger/remote-debugging.md)。

    > [!TIP]
    > 如果要附加到进程，但连接成功但看不到所需的进程，请**从所有用户中选择"显示进程"复选框**。 如果您在不同的用户帐户下连接，这将显示进程。

4. 如果这些步骤不能解决此错误，请参阅[无法访问远程计算机](#dns)。

## <a name="connection-request-was-rejected-by-the-remote-debugger"></a><a name="rejected"></a>远程调试器拒绝了连接请求

在 **"附加到进程**"对话框或项目属性中，请确保远程计算机名称和端口号与远程调试器窗口中显示的名称和端口号匹配。 如果不正确，请修复并重试。

如果这些值正确，并且消息提到 Windows**身份验证**模式，请检查远程调试器是否处于正确的身份验证模式（**工具>选项**）。

## <a name="the-connection-with-the-remote-endpoint-was-terminated"></a><a name="connection_terminated"></a>与远程终结点的连接已终止

如果要调试 Azure 应用服务应用，请尝试使用云资源管理器或服务器资源管理器中的[附加调试器](../debugger/remote-debugging-azure.md#remote_debug_azure_app_service)命令，而不是**附加到进程**。

如果使用 **"附加到进程"** 来调试：

1. 在 **"附加到进程**"对话框或项目属性中，请确保远程计算机名称和端口号与远程调试器窗口中显示的名称和端口号匹配。 如果不正确，请修复并重试。

2. 请查看服务器上的应用程序日志（Windows 上的事件查看器），以获取更多详细信息以帮助解决问题。

3. 否则，请尝试重新启动具有管理员权限的可视化工作室，然后重试。

## <a name="invalid-access-to-memory-location"></a><a name="invalid_access"></a>对内存位置的无效访问

发生了内部错误。 重新启动 Visual Studio，然后重试。

## <a name="there-is-no-server-by-the-specified-name-running-on-the-remote-computer"></a><a name="no_server"></a>远程计算机上没有按指定名称运行的服务器

可视化工作室无法连接到远程调试器。 此消息可能由于以下几个原因发生：

- 远程调试器可能在不同的用户帐户下运行。 请参阅[以下步骤](#user_accounts)

- 端口在防火墙上被阻止。 确保防火墙[未阻止您的请求](#firewall)，尤其是在使用第三方防火墙时。

- 远程调试器版本与可视化工作室不匹配。 要获取远程调试器的正确版本，请参阅[远程调试](../debugger/remote-debugging.md)。

## <a name="the-requested-name-was-valid-but-no-data-of-the-requested-type-was-found"></a><a name="valid_name"></a>请求的名称有效，但未找到请求类型的数据

远程计算机存在，但 Visual Studio 无法连接到远程调试器。 此消息可能由于以下几个原因发生：

- DNS 问题正在阻止连接。 请参阅[这些步骤](#dns)。

- 远程调试器可能在不同的用户帐户下运行。 按照[以下步骤操作](#user_accounts)。

- 端口在防火墙上被阻止。 确保防火墙[未阻止您的请求](#firewall)，尤其是在使用第三方防火墙时。

- 远程调试器版本与可视化工作室不匹配。 要获取远程调试器的正确版本，请参阅[远程调试](../debugger/remote-debugging.md)。

## <a name="the-visual-studio-remote-debugger-on-the-target-computer-cannot-connect-back-to-this-computer"></a><a name="cant_connect_back"></a>目标计算机上的可视化工作室远程调试器无法连接到此计算机

远程调试器可能在不同的用户帐户下运行。 在远程调试器中，打开 **"工具>将**用户添加到远程调试器的权限的权限。 有关详细信息，请参阅[远程调试器正在其他用户帐户下运行](#user_accounts)。

如果错误消息还提到防火墙，则本地计算机上的防火墙可能阻止远程计算机的通信回 Visual Studio。 请参阅[这些步骤](#firewall)。

## <a name="access-denied"></a><a name="access_denied"></a>访问被拒绝

如果您尝试从 32 位计算机（不支持）在 64 位远程计算机上调试，则可能会看到此错误。

## <a name="a-security-package-specific-error-occurred"></a><a name="security_package"></a>发生安全包特定错误

这可能是特定于 Windows XP 和 Windows 7 的旧问题。 请参阅[此信息](https://stackoverflow.com/questions/4786016/unable-to-connect-to-the-microsoft-remote-debugging-monitor-a-security-package)。

## <a name="causes-and-recommendations"></a>原因和建议

### <a name="the-remote-machine-is-not-reachable"></a><a name="dns"></a> 远程计算机不可访问

如果无法使用远程计算机名称进行连接，请尝试改用 IP 地址。 您可以在`ipconfig`远程计算机上的命令行中使用获取 IPv4 地址。 如果使用 HOSTS 文件，请验证该文件配置是否正确。

如果失败，请验证远程计算机在网络上是否可以访问[（ping](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee624059(v=ws.10))远程计算机）。 不支持通过 Internet 进行远程调试，但在某些 Microsoft Azure 方案中除外。

### <a name="the-server-name-is-incorrect-or-third-party-software-is-interfering-with-the-remote-debugger"></a><a name="server_incorrect"></a>服务器名称不正确或第三方软件干扰远程调试器

在 Visual Studio 中，查看项目属性并确保服务器名称正确。 请参阅[C# 和可视化基础](../debugger/remote-debugging-csharp.md#remote_csharp)和[C++](../debugger/remote-debugging-cpp.md#remote_cplusplus)的主题。 对于ASP.NET，根据项目类型打开**属性/Web /服务器**或**属性/调试**。

> [!NOTE]
> 如果要附加到进程，则不使用项目属性中的远程设置。

如果服务器名称正确，则防病毒软件或第三方防火墙可能阻止远程调试器。 在本地调试时，可能会发生这种情况，因为 Visual Studio 是一个 32 位应用程序，因此它使用 64 位版本的远程调试器来调试 64 位应用程序。 32 位和 64 位进程使用本地计算机中的本地网络进行通信。 计算机会持续进行网络通信，但第三方安全软件可能会阻止通信。

### <a name="the-remote-debugger-is-running-under-a-different-user-account"></a><a name="user_accounts"></a> 远程调试器使用不同的用户帐户运行

默认情况下，远程调试器将仅接受来自启动远程调试器的用户和管理员组成员的连接。 必须显式授予其他用户权限。

可通过下列方法之一解决此问题：

- 将 Visual Studio 用户添加到远程调试器的权限（在远程调试器窗口中，选择**工具>权限**）。

- 在远程计算机上，在 Visual Studio 计算机上使用的用户帐户和密码下重新启动远程调试器。

    > [!NOTE]
    > 如果在远程服务器上运行远程调试器，请右键单击远程调试器应用并选择 **"作为管理员运行**"（或者，可以将远程调试器作为服务运行）。 如果您没有在远程服务器上运行它，只需正常启动它。

- 可以使用“/allow \<username>”参数 `msvsmon /allow <username@computer>` 从命令行启动远程调试器****。

- 或者，您可以允许任何用户执行远程调试。 在远程调试器窗口中，转到“工具”>“选项”对话框****。 选中“无身份验证”   **** 后，可选中 ****“允许任何用户进行调试”。 但是，仅当其他选项失败或处于专用网络时，才应尝试此选项。

### <a name="the-firewall-on-the-remote-machine-doesnt-allow-incoming-connections-to-the-remote-debugger"></a><a name="firewall"></a> 远程计算机上的防火墙不允许对远程调试器使用传入连接
 Visual Studio 计算机上的防火墙和远程计算机上的防火墙都必须配置为允许在 Visual Studio 和远程调试器之间进行通信。 有关远程调试器使用的端口的信息，请参阅 [Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)。 有关配置 Windows 防火墙的信息，请参阅 [Configure the Windows Firewall for Remote Debugging](../debugger/configure-the-windows-firewall-for-remote-debugging.md)。

### <a name="the-version-of-the-remote-debugger-doesnt-match-the-version-of-visual-studio"></a>远程调试器的版本不匹配 Visual Studio 的版本
 在本地运行的 Visual Studio 的版本必须与远程计算机上运行的远程调试监视器的版本匹配。 若要解决此问题，请下载并安装匹配的远程调试监视器版本。 要获取远程调试器的正确版本，请参阅[远程调试](../debugger/remote-debugging.md)。

### <a name="the-local-and-remote-machines-have-different-authentication-modes"></a>本地和远程计算机具有不同的身份验证模式
 本地和远程计算机需要使用相同的身份验证模式。 若要解决此问题，请确保这两台计算机使用相同的身份验证模式。 您可以更改身份验证模式。 在远程调试器窗口中，转到 **"工具>选项"** 对话框。

 有关身份验证模式的详细信息，请参阅 [Windows 身份验证概述](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831472(v=ws.11))。

### <a name="anti-virus-software-is-blocking-the-connections"></a>防病毒软件正在阻止连接
 Windows 防病毒软件允许远程调试器连接，但某些第三方防病毒软件可能会阻止它们。 查看你防病毒软件的文档以了解如何允许这些连接。

### <a name="network-security-policy-is-blocking-communication-between-the-remote-machine-and-visual-studio"></a>网络安全策略阻塞远程计算机和 Visual Studio 之间的通信
 查看网络安全以确保它没有阻止通信。 有关 Windows 网络安全策略的详细信息，请参阅[安全策略设置](/windows/device-security/security-policy-settings/security-policy-settings)。

### <a name="the-network-is-too-busy-to-support-remote-debugging"></a>网络太忙无法支持远程调试
 你可能需要在另一个时间进行远程调试，或重新安排另一个时间进行网络上的工作。

## <a name="more-help"></a>更多帮助
 要获得更多远程调试器帮助，打开远程调试器的帮助页（**帮助>** 远程调试器中的使用情况）。

## <a name="see-also"></a>另请参阅
- [远程调试](../debugger/remote-debugging.md)
