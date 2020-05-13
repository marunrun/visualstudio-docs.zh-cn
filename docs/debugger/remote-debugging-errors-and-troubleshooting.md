---
title: 远程调试错误和故障排除 |微软文档
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301067"
---
# <a name="remote-debugging-errors-and-troubleshooting"></a>远程调试错误和疑难解答

尝试远程调试时，可能会遇到以下错误。

- [错误：无法自动单步执行服务器](../debugger/error-unable-to-automatically-step-into-the-server.md)

- [错误：Microsoft Visual Studio 远程调试监视器 (MSVSMON.EXE) 似乎没有在远程计算机上运行。](error-remote-debugging-monitor-msvsmon-exe-does-not-appear-to-be-running.md)

- [无法连接到 Microsoft Visual Studio 远程调试监视器](../debugger/unable-to-connect-to-the-microsoft-visual-studio-remote-debugging-monitor.md)

- [错误：远程计算机未显示在“远程连接”对话框中](../debugger/error-remote-machine-does-not-appear-in-a-remote-connections-dialog.md)

## <a name="run-the-remote-debugger-as-an-administrator"></a>以管理员身份运行远程调试器

如果不以管理员身份运行远程调试器，则可能会遇到问题。 例如，您可能会看到以下错误："可视化工作室远程调试器 （MSVSMON）。EXE） 没有足够的权限来调试此过程。 如果将远程调试器作为应用程序（而不是服务）运行，您可能会看到[不同的用户帐户](error-the-microsoft-visual-studio-remote-debugging-monitor-on-the-remote-computer-is-running-as-a-different-user.md)错误。

### <a name="when-running-the-remote-debugger-as-a-service"></a>将远程调试器作为服务运行时

将远程调试器作为服务运行时，我们建议将其作为管理员运行，原因如下：

- 远程调试器服务仅允许来自管理员的连接，因此没有**引入新的安全风险**，通过作为管理员运行它。

- 当 Visual Studio 用户比远程调试器本身拥有更多调试进程的权限时，它可以防止导致错误。

- 简化远程调试器的设置和配置。

虽然无需作为管理员运行远程调试器即可进行调试，但有几个要求使此调试正常工作，并且通常需要更高级的服务配置步骤。

- 您在远程计算机上使用的帐户必须具有**登录作为服务**权限。 请参阅[无法连接回](error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer.md)错误文章中的"将登录作为服务添加登录"下的步骤。

- 帐户必须具有调试目标进程的权限。 要获得这些权限，必须在与要调试的进程相同的帐户下运行远程调试器。 （更简单的替代方法是以管理员身份运行服务。 

- 帐户必须能够通过网络连接到 Visual Studio 计算机（即使用身份验证）。 在域上，如果远程调试器在内置本地系统或网络服务帐户或域帐户下运行，则更容易连接。 内置帐户具有更高的安全权限，可能会带来安全风险。

### <a name="when-running-the-remote-debugger-as-an-application-normal-mode"></a>当作为应用程序运行远程调试器时（正常模式）

如果您尝试附加到自己的非提升进程（如普通应用程序），则是否以管理员身份运行远程调试器并不重要。

您希望在以下几个方案中以管理员身份运行远程调试器：

- 您希望附加到以其他用户身份运行的进程（例如调试 IIS 时），或

- 您正在尝试启动另一个进程，并且要启动的过程是管理员。

如果要启动进程 **，则不想**以管理员身份运行，并且要启动的进程**不应**是管理员。

## <a name="see-also"></a>另请参阅
- [远程调试](../debugger/remote-debugging.md)