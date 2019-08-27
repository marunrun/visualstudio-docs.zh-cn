---
title: 错误：Kerberos 身份验证失败 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.callback_kerberos_auth_failed
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: c18053f9-9074-4bc3-a8bf-13e4acbea921
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b5e85bc7a5bac87692448aab393056fa1db5edbd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62535627"
---
# <a name="error-kerberos-authentication-failed"></a>错误：Kerberos 身份验证失败
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当尝试进行远程调试时，可能会收到以下错误消息：  
  
```  
Error: The Visual Studio Remote Debugger on the target computer cannot connect back to this computer. Kerberos auythentication failed.  
```  
  
 当 Visual Studio 远程调试监视器在“本地系统”帐户或“网络服务”帐户下运行时，会发生此错误。 在其中任何一个帐户下，远程调试器都必须建立 Kerberos 身份验证连接，以便向 Visual Studio 调试器主机提供反馈。  
  
 Kerberos 身份验证在下列条件下不可用：  
  
- 目标计算机或调试器主机位于工作组中，而不是位于域中  
  
   \- 或 -  
  
- 域控制器上已禁用 Kerberos。  
  
  如果 Kerberos 身份验证不可用，请更改用于运行 Visual Studio 远程调试监视器的帐户。 有关过程，请参阅[错误：目标计算机上的 Visual Studio 远程调试器服务无法重新连接到此计算机](../debugger/error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer.md)。  
  
  如果这两台计算机都连接到同一域，而您仍然收到此消息，请验证目标计算机上的 DNS 是否正确解析了调试器主机的名称。 请参见下面的步骤。  
  
### <a name="to-verify-that-dns-on-the-target-computer-is-correctly-resolving-the-debugger-host-computer-name"></a>验证目标计算机上的 DNS 是否正确解析了调试器主机名称  
  
1. 在目标计算机上打开**开始**菜单，依次指向**附件**，然后单击**命令提示符**。  
  
2. 在**命令提示符**窗口中，键入：  
  
    ```  
    ping <debugger_host_computer_name>  
    ```  
  
3. `ping` 响应的第一行显示了 DNS 为指定计算机返回的完整计算机名称和 IP 地址。  
  
4. 在调试器主机上，打开“命令提示符”窗口并运行 `ipconfig`。  
  
5. 比较 IP 地址值。  
  
## <a name="see-also"></a>请参阅  
 [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [远程调试](../debugger/remote-debugging.md)
