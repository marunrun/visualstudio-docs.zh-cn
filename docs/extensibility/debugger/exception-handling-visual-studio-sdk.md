---
title: 异常处理 (Visual Studio SDK) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], exception handling
ms.assetid: 7279dc16-db14-482c-86b8-7b3da5a581d2
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7fdb309c01979985d1c00eedab9c496d0af44e07
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66315270"
---
# <a name="exception-handling-visual-studio-sdk"></a>异常处理 (Visual Studio SDK)
下面介绍所发生异常时的过程。

## <a name="exception-handling-process"></a>异常处理过程

1. 当第一次引发异常，但它由正在调试的程序中的异常处理程序之前，调试引擎 (DE) 将发送[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)会话调试管理器 (SDM) 为停止事件。 `IDebugExceptionEvent2`要是异常 （在中调试包的异常对话框中指定） 的设置指定用户想要停止上首次异常通知的发送。

2. SDM 调用[IDebugExceptionEvent2::GetException](../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)获取异常的属性。

3. 调试包调用[IDebugExceptionEvent2::CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)以确定什么的选项，可以向用户显示。

4. 调试包要求用户如何通过打开最可能的异常对话框中处理异常。

5. 如果用户选择继续，将调用 SDM [IDebugExceptionEvent2::CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)。

    - 如果该方法返回 S_OK，调用[IDebugExceptionEvent2::PassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md)。

         或

         如果该方法返回 S_FALSE，该程序正在调试就会有第二个机会处理异常。

6. 如果正在调试的程序的第二次异常没有处理程序，将发送 DE`IDebugExceptionEvent2`到作为 SDM **EVENT_SYNC_STOP**。

7. 调试包要求用户如何通过打开最可能的异常对话框中处理异常。

8. 调试包调用[IDebugExceptionEvent2::CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)以确定什么的选项，可以向用户显示。

9. 调试包要求用户如何通过打开第二个可能发生的异常对话框中处理异常。

10. 如果该方法返回 S_OK，调用`IDebugExceptionEvent2::PassToDebuggee`。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)