---
title: Visual Studio SDK)  (处理异常 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], exception handling
ms.assetid: 7279dc16-db14-482c-86b8-7b3da5a581d2
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 38e646f032a12de48bbfb55b089462c7f8a4dd26
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152795"
---
# <a name="exception-handling-visual-studio-sdk"></a>异常处理 (Visual Studio SDK)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

下面描述了在引发异常时所发生的过程。  
  
## <a name="exception-handling-process"></a>异常处理过程  
  
1. 当首次引发异常时，但在被调试程序中的异常处理程序处理之前，调试引擎 (DE) 将 [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md) 发送到会话调试管理器 (SDM) 作为停止事件。 `IDebugExceptionEvent2`如果只有在调试包的 "异常" 对话框中指定的异常 (的设置，则将发送) 指定用户要在出现首次异常通知时停止。  
  
2. SDM 调用 [IDebugExceptionEvent2：： GetException](../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md) 以获取异常的属性。  
  
3. 调试包将调用 [IDebugExceptionEvent2：： CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) 来确定要向用户显示的选项。  
  
4. 调试包会要求用户如何通过打开 "首次异常" 对话框来处理异常。  
  
5. 如果用户选择继续，则 SDM 将调用 [IDebugExceptionEvent2：： CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)。  
  
    - 如果该方法返回 S_OK，则调用 [IDebugExceptionEvent2：:P asstodebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md)。  
  
         - 或 -  
  
         如果该方法返回 S_FALSE，则将为正在调试的程序提供另一个处理异常的机会。  
  
6. 如果正在调试的程序没有第二次异常的处理程序，则 DE 会将发送 `IDebugExceptionEvent2` 到 SDM 作为 **EVENT_SYNC_STOP**。  
  
7. 调试包会要求用户如何通过打开 "首次异常" 对话框来处理异常。  
  
8. 调试包将调用 [IDebugExceptionEvent2：： CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) 来确定要向用户显示的选项。  
  
9. 调试包通过打开第二个异常对话框来要求用户如何处理异常。  
  
10. 如果该方法返回 S_OK，则调用 `IDebugExceptionEvent2::PassToDebuggee` 。  
  
## <a name="see-also"></a>另请参阅  
 [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
