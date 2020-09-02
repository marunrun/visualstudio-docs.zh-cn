---
title: “为远程调试配置防火墙”对话框 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.firewallconfiguration
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
helpviewer_keywords:
- Configure Firewall for Remote Debugging dialog box
- remote debugging, configuring firewalls
- firewalls, configuring for remote debugging
ms.assetid: 5dff3393-fdeb-4129-a2f6-31f653107a82
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 26e2b1300feb8d2a15e63089ee9bddde5f2d1ef4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65702289"
---
# <a name="configure-firewall-for-remote-debugging-dialog-box"></a>“为远程调试配置防火墙”对话框
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当 Windows 防火墙阻止调试器通过网络接收信息时，会出现此对话框。 若要继续进行远程调试，则必须在防火墙上打开一个口以使调试器能够接收信息。  
  
> [!CAUTION]
> 如果在防火墙上打开一个入口，则可能会使计算机面临防火墙本应阻止的安全威胁。 在 Visual Studio 2015 中，打开一个入口进行远程调试会取消阻止端口 4020 和 4021。 其他版本的 Visual Studio 中会使用其他端口号。 有关详细信息，请参阅[远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)。 此外，这还允许调试器打开其他端口。 有关详细信息，请参阅[配置 Windows 防火墙以进行远程调试](../debugger/configure-the-windows-firewall-for-remote-debugging.md)。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **取消远程调试**  
 取消远程调试尝试。 计算机的安全设置保持不变。  
  
 **取消禁止从本地网络（子网）中的计算机进行远程调试的限制**  
 启用本地子网中的计算机的远程调试。 这可能会将安全漏洞暴露给本地子网上的计算机，但是防火墙将继续阻止来自子网外的信息。  
  
 **取消禁止从任何计算机进行远程调试的限制**  
 启用网络上任何位置的计算机的远程调试。 此设置是最不安全的。  
  
## <a name="see-also"></a>另请参阅  
 [调试器安全性](../debugger/debugger-security.md)   
 [在设备上设置远程工具](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)   
 [调试用户界面参考](../debugger/debugging-user-interface-reference.md)
