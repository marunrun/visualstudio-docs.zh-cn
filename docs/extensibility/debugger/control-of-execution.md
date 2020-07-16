---
title: 控件的执行 |Microsoft Docs
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
ms.openlocfilehash: 9c59831efb2fc97ad1bb2891fd93a67fe79f8eff
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2020
ms.locfileid: "86387000"
---
# <a name="control-of-execution"></a>控制执行
调试引擎（DE）通常会发送以下事件之一作为上一个启动事件：

- 如果附加到新启动的程序，则为入口点事件

- 加载完成事件（如果附加到已在运行的程序）

  这两个事件都将停止事件，这意味着，通过 IDE 来等待用户的响应。 有关详细信息，请参阅[运行模式](../../extensibility/debugger/operational-modes.md)。

## <a name="stopping-event"></a>正在停止事件
 向调试会话发送停止事件时：

1. 可以从事件接口获取包含当前指令指针的程序和线程。

2. IDE 确定当前源代码文件和位置，它在编辑器中显示为突出显示的位置。

3. 调试会话通常通过调用程序的**Continue**方法来响应第一次停止事件。

4. 然后，该程序将一直运行，直到遇到停止条件，如命中断点。 在这种情况下，将向调试会话发送一个断点事件。 断点事件是一个停止事件，并再次取消，以等待用户响应。

5. 如果用户想要单步执行、逐过程执行或跳出某个函数，IDE 将提示调试会话调用该程序的 `Step` 方法。 IDE 随后会传递步骤的单元（指令、语句或行）和步骤的类型（无论是单步执行、逐过程执行还是跳出函数）。 步骤完成后，将向调试会话发送一个步骤完成事件，该事件是一个停止事件。

    -或-

    如果用户想要继续从当前指令指针执行，IDE 将提示调试会话调用程序的**Execute**方法。 程序将继续执行，直到它遇到下一个停止条件为止。

    -或-

    如果调试会话要忽略特定的停止事件，调试会话会调用程序的**Continue**方法。 如果程序在遇到停止条件时进入、锁定或跳出某个函数，则会继续执行此步骤。

   以编程方式，当 DE 遇到停止条件时，它通过[IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)接口将此类停止事件作为[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)或[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)发送到会话调试管理器（SDM）。 DE 传递表示程序的[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)和[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)接口以及包含当前指令指针的线程。 SDM 调用[IDebugThread2：： EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)以获取顶层堆栈帧并调用[IDebugStackFrame2：： GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)来获取与当前指令指针关联的文档上下文。 此文档上下文通常是源代码文件名、行号和列号。 IDE 使用这些代码突出显示包含当前指令指针的源代码。

   SDM 通常通过调用[IDebugProgram2：： Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)响应此首次停止事件。 然后，该程序将一直运行，直到它遇到停止条件，如命中断点，在这种情况下，将[IDebugBreakpointEvent2 接口](../../extensibility/debugger/reference/idebugbreakpointevent2.md)发送到 SDM。 断点事件是一个停止事件，并再次取消，以等待用户响应。

   如果用户想要单步执行、逐过程执行或跳出某个函数，IDE 将提示 SDM 调用[IDebugProgram2：： step](../../extensibility/debugger/reference/idebugprogram2-step.md)。 然后，IDE 传递[STEPUNIT](../../extensibility/debugger/reference/stepunit.md) （指令、语句或行）和[STEPKIND](../../extensibility/debugger/reference/stepkind.md)，即，是单步执行、逐过程执行还是跳出函数。 步骤完成后，取消将[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)接口发送到 SDM，后者是一个停止事件。

   如果用户想要继续从当前指令指针执行，则 IDE 会要求 SDM 调用[IDebugProgram2：： Execute](../../extensibility/debugger/reference/idebugprogram2-execute.md)。 程序将继续执行，直到它遇到下一个停止条件为止。

   如果调试包要忽略特定的停止事件，则调试包将调用 SDM，这将调用[IDebugProgram2：： Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)。 如果程序在遇到停止条件时进入、锁定或跳出某个函数，则会继续执行此步骤。 这意味着程序将保留单步执行状态，以便它知道如何继续。

   SDM 进行的调用（即 `Step` **Execute**和**Continue** ）是异步的，这意味着 sdm 需要调用快速返回。 如果在执行、执行或继续返回之前，取消在同一线程上向 SDM 发送停止事件， `Step` 则 sdm 将停止响应。 **Execute** **Continue**

## <a name="see-also"></a>另请参阅
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
