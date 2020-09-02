---
title: 在出现异常之后继续执行 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
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
- managed exceptions, continuing execution after
- exceptions, continuing execution after
- debugger, exceptions
- managed code, exception handling
- exception handling, continuing execution after
- execution, continuing after an exception
- program execution
- threading [Visual Studio], continuing execution after exceptions
- Exceptions dialog box
- programs, executing
ms.assetid: 6fe97aac-2131-4615-bd92-d3afee741558
caps.latest.revision: 30
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6ae74c51f0f738bc596fbe5c789011630927707c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65702256"
---
# <a name="continuing-execution-after-an-exception"></a>在出现异常之后继续执行
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当调试器因出现异常而中断执行时，会显示一个对话框。 对于 Visual Basic 或 c #，默认情况下会显示 " [异常助手](https://msdn.microsoft.com/library/992892ac-9d52-44cc-bf09-b44bfc5befeb) " 对话框。 对于 c + +，你将看到 "旧 **异常** " 对话框。 如果使用 Visual Basic 或 c #，但在 "**选项**" 对话框中禁用了 "**异常助手**"，则会看到 "**异常**" 对话框。  
  
 出现 " **异常助手** " 或 " **异常** " 对话框时，您可以尝试修复导致异常的问题。  
  
## <a name="managed-code"></a>托管代码  
 在托管代码中，你可以在出现未经处理的异常后在同一线程内继续执行。 **异常助手**将调用堆栈展开到引发异常的点。  
  
## <a name="native-code"></a>本机代码  
 在本机 C/C++ 中，您有两个选项：  
  
- 您可以单击 " **中断** " 并尝试修复问题。 处于中断模式时，您可以通过在 " **调用堆栈** " 窗口中右键单击某一帧并在快捷菜单上选择 " **展开到此帧" 来** 展开调用堆栈。 当你继续调试时，如果你未解决该问题，则会再次出现 " **异常** " 对话框。 否则，" **异常** " 对话框将不会重新出现。  
  
- 你可以单击 " **继续** " 以继续执行，而不会尝试解决问题。 此时将重新出现 " **异常** " 对话框。  
  
## <a name="mixed-code"></a>混合代码  
 如果在调试由本机和托管代码混合而成的代码时遇到未经处理的异常，操作系统的约束会阻止调用堆栈的展开。 如果尝试使用快捷菜单来展开调用堆栈，则会出现一个错误消息，告诉你在混合代码调试期间，调试器无法在异常未得到处理的情况下展开调用堆栈。  
  
## <a name="see-also"></a>另请参阅  
 [管理调试器的异常](../debugger/managing-exceptions-with-the-debugger.md)
