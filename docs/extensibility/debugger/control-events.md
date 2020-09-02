---
title: 控制事件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: 0fc63484-5fb6-4887-9ea4-1905b459ca9d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bc2c3ad9c9b63923bdf2f107e7bc582f3c76cd62
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739085"
---
# <a name="control-events"></a>控件事件
你必须在程序的受控执行过程中发送事件。 所有事件都是使用 [IDebugEvent2](../../extensibility/debugger/reference/idebugevent2.md) 接口发送的，并且具有要求实现 [IDebugEvent2：： GetAttributes](../../extensibility/debugger/reference/idebugevent2-getattributes.md) 方法的属性。

## <a name="additional-methods"></a>其他方法
 某些事件需要实现其他方法，如下所示：

- 当调试引擎 (DE) 初始化时发送 [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) 接口要求您实现 [IDebugEngineCreateEvent2：： GetEngine](../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md) 方法。

- 执行控件要求将此类控件事件实现为 [IDebugBreakEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md) 和[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) 接口。 **IDebugBreakEvent2** 仅对异步中断是必需的。

- 单步执行函数需要实现 [IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) 接口及其方法。

  从断点派生的事件要求实现 [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)、 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)和 [IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) 接口，以及 [IDebugBreakpointBoundEvent2：： GetPendingBreakpoint](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md) 和 [EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md) 方法。

  异步表达式计算需要实现 [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) 接口及其 [IDebugExpressionEvaluationCompleteEvent2：： system.componentmodel.design.serialization.codedomserializerbase.getexpression](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)[和 GetResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md) 方法。

  同步事件需要实现 [IDebugEngine2：： ContinueFromSynchronousEvent](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md) 方法。

  为了让引擎编写字符串样式输出，必须实现 [IDebugOutputStringEvent2：： GetString](../../extensibility/debugger/reference/idebugoutputstringevent2-getstring.md) 方法。

## <a name="see-also"></a>另请参阅
- [执行控制和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)
