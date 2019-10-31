---
title: 远程调试错误和故障排除 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugger, errors
- debugging errors
- remote debugging, troubleshooting
- troubleshooting remote debugging
- errors [debugger], remote debugging
- remote debugging, errors
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8b413ce193e6761d515de5bc5ef30fae8e18a3a3
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73187514"
---
# <a name="remote-debugging-errors-and-troubleshooting"></a>远程调试错误和疑难解答

尝试远程调试时，可能会遇到以下错误。

- [Error: Unable to Automatically Step Into the Server](../debugger/error-unable-to-automatically-step-into-the-server.md)

- [错误：Microsoft Visual Studio 远程调试监视器 (MSVSMON.EXE) 似乎没有在远程计算机上运行。](error-remote-debugging-monitor-msvsmon-exe-does-not-appear-to-be-running.md)

- [Unable to Connect to the Microsoft Visual Studio Remote Debugging Monitor](../debugger/unable-to-connect-to-the-microsoft-visual-studio-remote-debugging-monitor.md)

- [错误：远程计算机未显示在“远程连接”对话框中](../debugger/error-remote-machine-does-not-appear-in-a-remote-connections-dialog.md)

## <a name="run-the-remote-debugger-as-an-administrator"></a>以管理员身份运行远程调试器

如果没有以管理员身份运行远程调试器，则可能会遇到问题。 例如，你可能会看到以下错误： "Visual Studio 远程调试器（MSVSMON。EXE）没有足够的特权，无法调试此进程。 " 如果将远程调试器作为应用程序（而不是服务）运行，你可能会看到[不同的用户帐户](error-the-microsoft-visual-studio-remote-debugging-monitor-on-the-remote-computer-is-running-as-a-different-user.md)错误。

### <a name="when-running-the-remote-debugger-as-a-service"></a>作为服务运行远程调试器时

在将远程调试器作为服务运行时，出于以下几个原因，我们建议以管理员身份运行它：

- 远程调试器服务只允许来自管理员的连接，因此以管理员身份运行它**不**会引入新的安全风险。

- 当 Visual Studio 用户拥有调试进程的权限超过远程调试器本身的权限时，它可以防止出现错误。

- 简化远程调试器的设置和配置。

尽管可以在不以管理员身份运行远程调试器的情况下进行调试，但有几个要求可以使此工作正确并经常需要更高级的服务配置步骤。

- 您在远程计算机上使用的帐户必须具有 "**作为服务登录**" 特权。 请参阅[无法连接回](error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer.md)错误一文中的 "添加作为服务登录" 下的步骤。

- 此帐户必须具有调试目标进程的权限。 若要获取这些权限，你必须在要调试的进程所用的帐户下运行远程调试器。 （更简单的方法是以管理员身份运行服务。） 

- 此帐户必须能够通过网络重新连接到 Visual Studio 计算机（即通过网络进行身份验证）。 在域中，如果远程调试器正在内置本地系统或网络服务帐户或域帐户下运行，则更容易连接回。 内置帐户的安全权限可能会带来安全风险。

### <a name="when-running-the-remote-debugger-as-an-application-normal-mode"></a>作为应用程序运行远程调试器时（正常模式）

如果你尝试附加到你自己的非提升进程（例如普通应用程序），则如果你以管理员身份运行远程调试器，这并不重要。

需要在多个方案中以管理员身份运行远程调试器：

- 要附加到作为另一个用户运行的进程（例如调试 IIS 时），或

- 你正在尝试启动另一个进程，而你要启动的进程是管理员。

如果你想要启动进程，并且你想要启动的进程**不**应是管理员，则**不**希望以管理员身份运行。

## <a name="see-also"></a>请参阅
- [Remote Debugging](../debugger/remote-debugging.md)