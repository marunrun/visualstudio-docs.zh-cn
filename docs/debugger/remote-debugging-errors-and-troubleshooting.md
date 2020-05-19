---
title: 远程调试错误和疑难解答 | Microsoft Docs
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
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301067"
---
# <a name="remote-debugging-errors-and-troubleshooting"></a>远程调试错误和疑难解答

尝试远程调试时，可能会遇到下列错误。

- [错误：无法自动单步执行服务器](../debugger/error-unable-to-automatically-step-into-the-server.md)

- [错误：Microsoft Visual Studio 远程调试监视器 (MSVSMON.EXE) 似乎没有在远程计算机上运行。](error-remote-debugging-monitor-msvsmon-exe-does-not-appear-to-be-running.md)

- [Unable to Connect to the Microsoft Visual Studio Remote Debugging Monitor](../debugger/unable-to-connect-to-the-microsoft-visual-studio-remote-debugging-monitor.md)

- [错误：远程计算机未显示在“远程连接”对话框中](../debugger/error-remote-machine-does-not-appear-in-a-remote-connections-dialog.md)

## <a name="run-the-remote-debugger-as-an-administrator"></a>以管理员身份运行远程调试器

如果不以管理员身份运行远程调试器，则可能会遇到问题。 例如，可能会看到以下错误：“Visual Studio 远程调试器 (MSVSMON.EXE) 没有足够的特权，无法调试此进程。” 如果将远程调试器作为应用程序（而不是服务）运行，则可能会看到[其他用户帐户](error-the-microsoft-visual-studio-remote-debugging-monitor-on-the-remote-computer-is-running-as-a-different-user.md)错误。

### <a name="when-running-the-remote-debugger-as-a-service"></a>将远程调试器作为服务运行

将远程调试器作为服务运行时，我们出于以下几个原因建议以管理员身份运行它：

- 远程调试器服务仅允许来自管理员的连接，因此，以管理员身份运行它时不会带来新的安全风险。

- 当 Visual Studio 用户拥有的进程调试权限比远程调试器本身拥有的进程调试权限更多时，可防止由此导致的错误。

- 简化远程调试器的设置和配置。

尽管可以在不以管理员身份运行远程调试器的情况下进行调试，但需要满足多个要求才能正常工作，并且它们通常需要执行更高级的服务配置步骤。

- 在远程计算机上使用的帐户必须具有“作为服务登录”特权。 请参阅[无法重新连接](error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer.md)错误文章中“将登录作为服务添加”下的步骤。

- 该帐户必须具有调试目标进程的权限。 若要获得这些权限，必须使用与要调试的进程所用帐户相同的帐户运行远程调试器。 （更简便的替代方法是以管理员身份运行服务。） 

- 该帐户必须能够通过网络重新连接到 Visual Studio 计算机（即向其进行身份验证）。 在域中，如果远程调试器在内置的本地系统/网络服务帐户或域帐户下运行，则更容易重新连接。 内置帐户具有提升的安全特权，这可能带来安全风险。

### <a name="when-running-the-remote-debugger-as-an-application-normal-mode"></a>将远程调试器作为应用程序运行（正常模式）

如果尝试附加到自己的非提升进程（例如普通应用程序），则是否以管理员身份运行远程调试器无关紧要。

你需要在多种方案中以管理员身份运行远程调试器：

- 想要附加到以其他用户身份运行的进程（例如调试 IIS 时），或者

- 正在尝试启动另一个进程，且要启动的进程需要以管理员身份运行。

如果你想要启动进程，且你想要启动的进程不应以管理员身份运行，则无需以管理员身份运行。

## <a name="see-also"></a>请参阅
- [远程调试](../debugger/remote-debugging.md)