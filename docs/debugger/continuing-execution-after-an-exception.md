---
title: 在出现异常后继续执行 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e7be214a950c8cc93d986f97834a848bd9ab824e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745649"
---
# <a name="continuing-execution-after-an-exception"></a>在出现异常之后继续执行
当调试器因异常而中断执行时，默认情况下，你将看到**异常帮助器**。 如果你已在**选项**对话框中禁用了**异常帮助器**，将看到**异常助手**（C# 或 Visual Basic）或**异常**对话框 (C++)。

 出现**异常帮助**程序时，您可以尝试修复导致异常的问题。

## <a name="managed-and-native-code"></a>托管代码和本机代码
 在托管代码和本机代码中，你可以在发生了未经处理的异常后继续在同一线程内执行。 异常帮助器会将调用堆栈展开到抛出异常的位置。

## <a name="mixed-code"></a>混合代码
 如果在调试由本机和托管代码混合而成的代码时遇到未经处理的异常，操作系统的约束会阻止调用堆栈的展开。 如果尝试使用快捷菜单来展开调用堆栈，则会出现一个错误消息，告诉你在混合代码的调试期间，调试器无法在异常未得到处理的情况下展开调用堆栈。

## <a name="see-also"></a>请参阅

- [管理调试器的异常](../debugger/managing-exceptions-with-the-debugger.md)