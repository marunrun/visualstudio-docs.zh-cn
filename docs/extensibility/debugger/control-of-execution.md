---
title: 执行控制 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], control of execution
ms.assetid: 97071846-007e-450f-95a6-f072d0f5e61e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e2d338c5470611a5eea0c6279404c4eaddebb2d0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739074"
---
# <a name="control-of-execution"></a>执行控制
调试引擎 （DE） 通常作为上次启动事件发送以下事件之一：

- 入口点事件（如果附加到新启动的程序）

- 负载完成事件（如果附加到已运行的程序）

  这两个事件都停止事件，这意味着 DE 通过 IDE 等待用户的响应。 有关详细信息，请参阅[操作模式](../../extensibility/debugger/operational-modes.md)。

## <a name="stopping-event"></a>停止事件
 当停止事件发送到调试会话时：

1. 可以从事件接口获取包含当前指令指针的程序和线程。

2. IDE 确定当前源代码文件和位置，该文件和位置在编辑器中显示为突出显示。

3. 调试会话通常通过调用程序的 **"继续"** 方法响应此第一个停止事件。

4. 然后，程序运行，直到它遇到停止条件，如击中断点。 在这种情况下，DE 向调试会话发送断点事件。 断点事件是停止事件，DE 再次等待用户响应。

5. 如果用户选择踏入、执行或退出函数，IDE 会提示调试会话调用程序`Step`的方法。 然后，IDE 传递步进单元（指令、语句或行）和步进类型（是步进、执行还是退出函数）。 步骤完成后，DE 会向调试会话发送一个步骤完成事件，调试会话是停止事件。

    \- 或 -

    如果用户选择继续从当前指令指针执行，IDE 会提示调试会话调用**程序的执行方法**。 程序恢复执行，直到遇到下一个停止条件。

    \- 或 -

    如果调试会话要忽略特定的停止事件，则调试会话将调用程序的 **"继续"** 方法。 如果程序在遇到停止条件时步进、越过或退出函数，则继续执行此步骤。

   在编程上，当 DE 遇到停止条件时，它会通过[IDebugEvent 回调 2](../../extensibility/debugger/reference/idebugeventcallback2.md)接口向会话调试管理器 （SDM） 发送[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)或[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)等停止事件。 DE 传递[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)和[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)接口，这些接口表示程序和包含当前指令指针的线程。 SDM 调用[IDebugThread2：enumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)获取顶部堆栈帧，并调用[IDebugStackFrame2：：：获取文档上下文](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)以获取有关当前指令指针的文档上下文。 此文档上下文通常是源代码文件名、行号和列号。 IDE 使用这些突出显示包含当前指令指针的源代码。

   SDM 通常通过调用[IDebugProgram2：：继续](../../extensibility/debugger/reference/idebugprogram2-continue.md)来响应第一个停止事件。 然后，程序运行，直到它遇到停止条件，如击中断点，在这种情况下，DE 向 SDM 发送[IDebugBreakpointEvent2 接口](../../extensibility/debugger/reference/idebugbreakpointevent2.md)。 断点事件是停止事件，DE 再次等待用户响应。

   如果用户选择踏入、执行或退出函数，IDE 将提示 SDM 调用[IDebugProgram2：：步骤](../../extensibility/debugger/reference/idebugprogram2-step.md)。 然后，IDE 传递[STEPUNIT（](../../extensibility/debugger/reference/stepunit.md)指令、语句或行）和[STEPKIND，](../../extensibility/debugger/reference/stepkind.md)即是步进、执行还是退出函数。 步骤完成后，DE 会向 SDM 发送[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)接口，这是一个停止事件。

   如果用户选择继续从当前指令指针执行，IDE 会要求 SDM 调用[IDebugProgram2：：：执行](../../extensibility/debugger/reference/idebugprogram2-execute.md)。 程序恢复执行，直到遇到下一个停止条件。

   如果调试包要忽略特定的停止事件，调试包将调用 SDM，它调用[IDebugProgram2：：：继续](../../extensibility/debugger/reference/idebugprogram2-continue.md)。 如果程序在遇到停止条件时步进、执行或退出函数，则继续执行此步骤。 这意味着程序保持步进状态，以便它知道如何继续。

   SDM 对`Step`**的调用**是异步的**Continue**，这意味着 SDM 希望调用快速返回。 如果 DE 在 "**执行 "或****"继续**返回"`Step`之前在同一线程上向 SDM 发送停止事件，则 SDM 挂起。

## <a name="see-also"></a>请参阅
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
