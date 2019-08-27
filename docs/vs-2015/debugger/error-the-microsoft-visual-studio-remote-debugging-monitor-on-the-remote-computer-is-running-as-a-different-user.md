---
title: 错误：Microsoft Visual Studio 远程调试监视器在远程计算机上运行其他用户的身份 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- -anyuser option
- anyuser option
- Remote Debugging Monitor
- remote debugging, Remote Debugging Monitor
- msvsmon.exe
ms.assetid: e5b18734-2daf-4c58-b5de-24ae1295703e
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: dffaafbca80828a7501f5f7d24e525225284f5a8
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697314"
---
# <a name="error-the-microsoft-visual-studio-remote-debugging-monitor-on-the-remote-computer-is-running-as-a-different-user"></a>错误：远程计算机上的 Microsoft Visual Studio 远程调试监视器正在以其他用户身份运行 |Microsoft Docs
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当尝试执行远程调试时，您可能会收到如下错误信息：  
  
 远程计算机上的“Microsoft Visual Studio 远程调试监视器”正在以其他用户身份运行。  
  
## <a name="cause"></a>原因  
 如果正在“无身份验证”模式下进行调试，而启动 msvsmon 的用户不是运行 Visual Studio 的用户，则会收到此消息。  
  
## <a name="solution"></a>解决方案  
 最安全最好的解决方案是，使用运行 Visual Studio 时所用的用户帐户运行远程调试监视器 (msvsmon.exe)。 如果无法做到这一点，可以通过在远程调试监视器“选项”对话框中选择“允许任何用户进行调试”，使用其他用户帐户运行远程调试监视器。   
  
> [!CAUTION]
> 授予其他用户进行连接的权限可能会导致意外地连接到错误的远程调试会话。 在“无身份验证”模式中调试不安全，应谨慎使用。  
  
 有关详细信息，请参阅[启动远程调试监视器](https://msdn.microsoft.com/library/55b60ce7-834b-4e83-a10e-fe4248260a4c)。  
  
## <a name="see-also"></a>请参阅  
 [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [远程调试](../debugger/remote-debugging.md)
