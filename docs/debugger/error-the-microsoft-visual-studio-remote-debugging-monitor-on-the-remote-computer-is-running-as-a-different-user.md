---
title: 错误：远程计算机上的 Microsoft Visual Studio 远程调试监视器正在以其他用户身份运行 |Microsoft Docs
titleSuffix: ''
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: troubleshooting
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- -anyuser option
- anyuser option
- Remote Debugging Monitor
- remote debugging, Remote Debugging Monitor
- msvsmon.exe
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b5ff383b279bbdac85ce85de6e65b857cec6a8e7
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72737479"
---
# <a name="error-the-microsoft-visual-studio-remote-debugging-monitor-on-the-remote-computer-is-running-as-a-different-user"></a>错误：远程计算机上的 Microsoft Visual Studio 远程调试监视器正在以其他用户身份运行 |Microsoft Docs
当尝试执行远程调试时，您可能会收到如下错误信息：

 远程计算机上的“Microsoft Visual Studio 远程调试监视器”正在以其他用户身份运行。

## <a name="cause"></a>原因
 如果正在“无身份验证”模式下进行调试，而启动 msvsmon 的用户不是运行 Visual Studio 的用户，则会收到此消息。

## <a name="solution"></a>解决方案
 最安全最好的解决方案是，使用运行 Visual Studio 时所用的用户帐户运行远程调试监视器 (msvsmon.exe)。 如果无法做到这一点，可以通过在远程调试监视器“选项”对话框中选择“允许任何用户进行调试”，使用其他用户帐户运行远程调试监视器   。 

> [!CAUTION]
> 授予其他用户进行连接的权限可能会导致意外地连接到错误的远程调试会话。 在“无身份验证”模式中调试不安全，应谨慎使用  。

## <a name="see-also"></a>请参阅
- [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)
- [远程调试](../debugger/remote-debugging.md)