---
title: 异常处理（可视化工作室 SDK） |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], exception handling
ms.assetid: 7279dc16-db14-482c-86b8-7b3da5a581d2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 34b83c7181a7ba405e642d9911e2c53df3f4401d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738760"
---
# <a name="exception-handling-visual-studio-sdk"></a>异常处理（可视化工作室 SDK）
下面描述了引发异常时发生的过程。

## <a name="exception-handling-process"></a>异常处理过程

1. 首次引发异常，但在调试程序中的异常处理程序处理异常之前，调试引擎 （DE） 会将[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)作为停止事件发送到会话调试管理器 （SDM）。 如果`IDebugExceptionEvent2`仅异常的设置（在调试包中的"例外"对话框中指定）指定用户希望在首次机会异常通知时停止，则将发送 。

2. SDM 调用[IDebugexceptionEvent2：：获取异常](../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)获取异常属性。

3. 调试包调用[IDebugexceptionEvent2：：CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)以确定要向用户呈现哪些选项。

4. 调试包询问用户如何通过打开第一个异常对话框来处理异常。

5. 如果用户选择继续，SDM 将调用[IDebugexceptionevent2：：CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)。

    - 如果该方法返回S_OK，则调用[IDebugexceptionEvent2：:PasstoDebuggee。](../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md)

         \- 或 -

         如果方法返回S_FALSE，则正在调试的程序将第二次处理异常。

6. 如果正在调试的程序没有第二个异常的处理程序，则 DE 将 a`IDebugExceptionEvent2`发送到 SDM 作为**EVENT_SYNC_STOP**。

7. 调试包询问用户如何通过打开第一个异常对话框来处理异常。

8. 调试包调用[IDebugexceptionEvent2：：CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)以确定要向用户呈现哪些选项。

9. 调试包询问用户如何通过打开第二个异常对话框来处理异常。

10. 如果方法返回S_OK，则调用`IDebugExceptionEvent2::PassToDebuggee`。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
