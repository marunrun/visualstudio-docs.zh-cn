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
ms.openlocfilehash: 078551111223f11b38f3192075caa9ddfabaf18c
ms.sourcegitcommit: 9753c7544cec852ca5efd0834e0956d9e53a5734
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "67043343"
---
# <a name="remote-debugging-errors-and-troubleshooting"></a>远程调试错误和疑难解答

尝试进行远程调试时，可能会遇到以下错误。

- [错误：无法自动单步执行服务器](../debugger/error-unable-to-automatically-step-into-the-server.md)

- [错误：Microsoft Visual Studio 远程调试监视器 (MSVSMON.EXE) 似乎没有在远程计算机上运行。](/visualstudio/debugger/error-remote-debugging-monitor-msvsmon-exe-does-not-appear-to-be-running)

- [Unable to Connect to the Microsoft Visual Studio Remote Debugging Monitor](../debugger/unable-to-connect-to-the-microsoft-visual-studio-remote-debugging-monitor.md)

- [错误：远程计算机未显示在“远程连接”对话框中](../debugger/error-remote-machine-does-not-appear-in-a-remote-connections-dialog.md)

## <a name="run-the-remote-debugger-as-an-administrator"></a>以管理员身份运行远程调试器

如果您不以管理员身份运行远程调试器，可能会遇到问题。 例如，可能会看到以下错误："Visual Studio 远程调试器 (MSVSMON。EXE) 有权限不足，无法调试此进程"。 如果为应用程序 （而不是服务） 正在运行远程调试器，您可能会看到[其他用户帐户](error-the-microsoft-visual-studio-remote-debugging-monitor-on-the-remote-computer-is-running-as-a-different-user.md)错误。

### <a name="when-running-the-remote-debugger-as-a-service"></a>远程调试器作为服务运行时

当远程调试器作为 s 服务运行，我们建议以管理员身份运行有几个原因：

- 远程调试器服务仅允许从连接管理员，因此没有**没有**引入通过以管理员身份运行的新安全风险。

- 它可能会阻止在 Visual Studio 用户有更多权利，若要调试的进程与远程调试器本身时的结果执行的错误。

- 若要简化的安装和配置远程调试器。

虽然可能无需以管理员身份运行远程调试器进行调试，但有几个要求，以便正确正常工作并且通常需要更高级的服务的配置步骤。

- 在远程计算机使用的帐户必须具有**作为服务登录**特权。 请参阅中的"添加登录即服务"下的步骤[无法重新连接](error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer.md)错误文章。

- 该帐户必须有权调试目标进程。 若要获取这些权限，必须以要进行调试的进程运行在同一帐户下的远程调试器。 （更轻松的替代方法是以管理员身份运行服务。） 

- 该帐户必须能够连接回 （即，使用进行身份验证） 的 Visual Studio 计算机在网络上。 在域中，它是可以轻松地将内置 Local System 或 Network Service 帐户或域帐户下运行远程调试器时。 内置帐户具有提升的可能会造成安全风险的安全特权。

### <a name="when-running-the-remote-debugger-as-an-application-normal-mode"></a>作为应用程序 （普通模式） 运行远程调试器

如果想要将附加到你自己的非提升进程 （如普通应用程序），它并不重要如果以管理员身份运行远程调试器。

你想要以管理员身份在多种方案中运行远程调试器：

- 你想要将附加到以其他用户身份运行的进程 (例如调试 IIS)，或

- 尝试启动另一个进程，并且你想要启动的过程是的管理员。

执行操作**不**想要以管理员身份运行，如果想要启动进程，并且你想要启动的过程应**不**是管理员。

## <a name="see-also"></a>请参阅
- [远程调试](../debugger/remote-debugging.md)