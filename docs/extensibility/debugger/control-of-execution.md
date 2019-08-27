---
title: 控制执行 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], control of execution
ms.assetid: 97071846-007e-450f-95a6-f072d0f5e61e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0d7594b91c67fb77d02e238a9336beb8d939714e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345526"
---
# <a name="control-of-execution"></a>控制执行
调试引擎 (DE) 通常情况下发送以下事件之一作为最后一个启动事件：

- 入口点事件，如果将附加到新启动的程序

- 加载完成事件，如果附加到已在运行的程序

  这两个这些事件包括停止事件，这意味着 DE 通过 IDE 等待来自用户的响应。 有关详细信息，请参阅[操作模式](../../extensibility/debugger/operational-modes.md)。

## <a name="stopping-event"></a>停止事件
 当停止事件发送到调试会话：

1. 可以从事件接口获得程序和包含当前指令指针的线程。

2. IDE 确定当前的源代码文件和位置，它将显示在编辑器中突出显示的那样。

3. 调试会话通常响应此第一个停止事件通过调用程序的**继续**方法。

4. 直到它遇到停止条件，例如命中断点，然后在运行该程序。 在这种情况下，DE 将断点事件发送到调试会话。 断点事件是停止事件，并 DE 再次等待用户响应。

5. 如果用户选择进入、 结束，或跳出函数，IDE 会提示以调用程序的调试会话`Step`方法。 然后，IDE 将传递的步骤 （指令、 语句或行） 和步骤 （无论是以单步执行、 逐过程或函数） 的类型的单位。 步骤完成后，DE 将发送到调试会话，这是停止事件的步骤完成事件。

    或

    如果用户选择继续执行从当前指令指针，IDE 将调试会话才能调用该程序的提示**Execute**方法。 程序继续执行，直到它遇到下一个停止条件。

    或

    如果在调试会话将忽略特定 stopping 事件，该调试会话将调用程序的**继续**方法。 如果该程序单步执行到、 逐过程或函数时遇到的停止条件，然后将继续步骤。

   以编程方式，当 DE 遇到停止条件，它会发送作为此类停止事件[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)或[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)会话调试管理器 (SDM) 通过[IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)接口。 DE pass [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)并[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)表示的程序和其中包含当前指令指针的线程的接口。 SDM 调用[IDebugThread2::EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)若要获取的堆栈帧和调用[IDebugStackFrame2::GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)若要获取当前指令与关联的文档上下文指针。 此文档上下文中通常是一个源的代码文件名称、 行和列号。 IDE 使用这些来突出显示包含当前指令指针的源代码。

   SDM 通常响应此第一个停止事件通过调用[IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)。 然后程序在运行，直到它遇到停止条件，例如命中的断点，在其中用例 DE 将发送[IDebugBreakpointEvent2 接口](../../extensibility/debugger/reference/idebugbreakpointevent2.md)到 SDM。 断点事件是停止事件，并 DE 再次等待用户响应。

   如果用户选择进入、 结束，或跳出函数，IDE 将提示来调用 SDM [IDebugProgram2::Step](../../extensibility/debugger/reference/idebugprogram2-step.md)。 然后，IDE 将传递[STEPUNIT](../../extensibility/debugger/reference/stepunit.md) （指令、 语句或行） 和[STEPKIND](../../extensibility/debugger/reference/stepkind.md)，即，是否要单步执行、 逐过程或函数。 完成该步骤时，将发送 DE [IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) SDM，即停止事件的接口。

   如果用户选择继续执行从当前指令指针，IDE 会要求 SDM 来调用[IDebugProgram2::Execute](../../extensibility/debugger/reference/idebugprogram2-execute.md)。 程序继续执行，直到它遇到下一个停止条件。

   调试包调试包，若要忽略特定的停止事件，如果调用 SDM，调用[IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)。 如果该程序单步执行到、 逐过程或函数时遇到的停止条件，它将继续步骤。 这意味着程序维护的单步执行状态，以便让它知道如何继续进行操作。

   SDM 对的调用`Step`， **Execute**，和**继续**是异步的这意味着 SDM 需要快速返回的调用。 如果 DE 发送 SDM stopping 事件之前的同一线程上`Step`， **Execute**，或**继续**返回 SDM 挂起。

## <a name="see-also"></a>请参阅
- [调试任务](../../extensibility/debugger/debugging-tasks.md)