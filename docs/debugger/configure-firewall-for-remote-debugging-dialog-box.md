---
title: "\"为远程调试配置防火墙\" 对话框 |Microsoft Docs"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.firewallconfiguration
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- Configure Firewall for Remote Debugging dialog box
- remote debugging, configuring firewalls
- firewalls, configuring for remote debugging
ms.assetid: 5dff3393-fdeb-4129-a2f6-31f653107a82
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8a2511fc2adfa63ff28f8459f48cbdf4b4623ff5
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745663"
---
# <a name="configure-firewall-for-remote-debugging-dialog-box"></a>“为远程调试配置防火墙”对话框
当 Windows 防火墙阻止调试器通过网络接收信息时，会出现此对话框。 若要继续进行远程调试，则必须在防火墙上打开一个口以使调试器能够接收信息。

> [!CAUTION]
> 如果在防火墙上打开一个入口，则可能会使计算机面临防火墙本应阻止的安全威胁。 在 Visual Studio 2015 中，打开一个入口进行远程调试会取消阻止端口 4020 和 4021。 其他版本的 Visual Studio 中会使用其他端口号。 有关详细信息，请参阅[远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)。 此外，这还允许调试器打开其他端口。 有关详细信息，请参阅[配置 Windows 防火墙以进行远程调试](../debugger/configure-the-windows-firewall-for-remote-debugging.md)。

## <a name="uielement-list"></a>UIElement 列表
 **取消远程调试**取消远程调试尝试。 计算机的安全设置保持不变。

 **取消阻止来自本地网络（子网）上的计算机的远程调试**启用本地子网上计算机的远程调试。 这可能会将安全漏洞暴露给本地子网上的计算机，但是防火墙将继续阻止来自子网外的信息。

 **取消阻止来自任何计算机的远程调试**启用对网络上任何位置的计算机的远程调试。 此设置是最不安全的。

## <a name="see-also"></a>请参阅

- [调试器安全](../debugger/debugger-security.md)
- [Remote Debugging](../debugger/remote-debugging.md)
- [调试用户界面参考](../debugger/debugging-user-interface-reference.md)