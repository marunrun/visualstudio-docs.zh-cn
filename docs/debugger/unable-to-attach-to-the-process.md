---
title: 无法附加到进程 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.remote.unable2attach
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
ms.openlocfilehash: 22d798d30d09cb509f53d093ae61bb1a02b414ec
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72728877"
---
# <a name="unable-to-attach-to-the-process"></a>无法附加到进程
无法附加到进程。 在连接到此计算机期间服务器上的调试器组件接收了被拒绝的访问。

 导致此错误的常见方案有两个：

 **方案 1：** 计算机 A 运行 Windows XP。 计算机 B 正在运行 Windows Server 2003。 计算机 B 上的注册表包含以下 DWORD 值：

 `HKLM\Software\Microsoft\MachineDebugManager\AllowLaunchAsOtherUser=1`

 用户 1 在计算机 B 上启动“终端服务器”会话（会话 1）并从该会话中启动托管应用程序。

 用户2（这两台计算机上的管理员）登录到计算机 A。然后，他或她尝试附加到在计算机 B 上的会话1中运行的应用程序。

 **方案 2：** 一位用户在位于同一工作组中的两台计算机 A 和 B 上使用同一密码登录到这两台计算机上。 调试器正在计算机 A 上运行，并尝试附加到在计算机 B 上运行的托管应用程序。计算机 A 具有**网络访问：本地帐户的共享和安全模式**设置为**来宾**。

### <a name="to-solve-scenario-1"></a>解决方案 1

- 在同一用户帐户名和密码下运行调试器和托管应用程序。

### <a name="to-solve-scenario-2"></a>解决方案 2

1. 从“开始”菜单中，选择“控制面板”。

2. 在“控制面板”中双击“管理工具”。

3. 在“管理工具”窗口中双击“本地安全策略”。

4. 在“本地安全策略”窗口中，选择“本地策略”。

5. 在“策略”列中，双击“网络访问: 本地帐户的共享和安全模型”。

6. 在“网络访问: 本地帐户的共享和安全模型”对话框中，将本地安全设置更改为“传统型”并单击“确定”。

    > [!CAUTION]
    > 将安全模型更改为“传统型”可能会导致对共享文件和 DCOM 组件的意外访问。 如果进行此更改，则远程用户可以使用您的本地用户帐户（而不是“来宾”）进行身份验证。 如果远程用户与你的用户名和密码匹配，则该用户将可以访问你已共享的任何文件夹或 DCOM 对象。如果使用此安全模型，请确保计算机上的所有用户帐户都具有强密码，或者为调试和调试的计算机设置隔离的网络孤岛以防止未经授权的访问。

7. 关闭所有窗口。

## <a name="see-also"></a>请参阅
- [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)