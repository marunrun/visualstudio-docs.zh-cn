---
title: '错误: Kerberos 身份验证失败 | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.callback_kerberos_auth_failed
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
ms.openlocfilehash: fbe13fd3d0dc7e29fc12d369ec0865bcbc97b1a4
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72737672"
---
# <a name="error-kerberos-authentication-failed"></a>错误：Kerberos 身份验证失败
当尝试进行远程调试时，可能会收到以下错误消息：

```cmd
Error: The Visual Studio Remote Debugger on the target computer cannot connect back to this computer. Kerberos authentication failed.
```

 当 Visual Studio 远程调试监视器在“本地系统”帐户或“网络服务”帐户下运行时，会发生此错误。 在其中任何一个帐户下，远程调试器都必须建立 Kerberos 身份验证连接，以便向 Visual Studio 调试器主机提供反馈。

 Kerberos 身份验证在下列条件下不可用：

- 目标计算机或调试器主机位于工作组中，而不是位于域中

   \- 或 -

- 域控制器上已禁用 Kerberos。

  如果 Kerberos 身份验证不可用，请更改用于运行 Visual Studio 远程调试监视器的帐户。 有关过程，请参阅[错误：目标计算机上的 Visual Studio 远程调试器服务无法重新连接到此计算机](../debugger/error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer.md)。

  如果这两台计算机都连接到同一域，而您仍然收到此消息，请验证目标计算机上的 DNS 是否正确解析了调试器主机的名称。 请参见下面的步骤。

### <a name="to-verify-that-dns-on-the-target-computer-is-correctly-resolving-the-debugger-host-computer-name"></a>验证目标计算机上的 DNS 是否正确解析了调试器主机名称

1. 在目标计算机上，打开“开始”菜单，指向“附件”，再单击“命令提示符”。

2. 在命令提示符窗口中，键入以下内容：

    ```cmd
    ping <debugger_host_computer_name>
    ```

3. `ping` 响应的第一行显示了 DNS 为指定计算机返回的完整计算机名称和 IP 地址。

4. 在调试器主机上，打开“命令提示符”窗口并运行 `ipconfig`。

5. 比较 IP 地址值。

## <a name="see-also"></a>请参阅
- [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)
- [Remote Debugging](../debugger/remote-debugging.md)
