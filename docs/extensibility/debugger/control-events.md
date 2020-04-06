---
title: 控制事件 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739085"
---
# <a name="control-events"></a>控制事件
您必须在程序的受控执行期间发送事件。 所有事件都使用[IDebugEvent2](../../extensibility/debugger/reference/idebugevent2.md)接口发送，并且具有需要您实现[IDebugEvent2：：getAttributes](../../extensibility/debugger/reference/idebugevent2-getattributes.md)方法的属性。

## <a name="additional-methods"></a>其他方法
 某些事件需要实现其他方法，如下所示：

- 当调试引擎 （DE） 初始化时，发送[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)接口需要实现[IDebugEngineCreateEvent2：getEngine](../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md)方法。

- 执行控制需要实现[IDebugBreakEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md)和[IDebugStepcompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)接口等控制事件。 **IDebugBreakEvent2**仅适用于异步中断。

- 进入函数需要实现[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)接口及其方法。

  从断点派生的事件需要实现[IDebugBreakpointErrorEvent2、IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)和[IDebugBreakpoint事件2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)接口，以及[IDebugBreakpointBoundEvent2：获取挂起的断点](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)点和[EnumBoundBreakpoint 方法](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)。 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)

  异步表达式计算要求您实现[IDebugExpression 表达式评估完成事件2 接口](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)及其[IDebugExpression 表达式评估完成事件2：：获取表达式](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)[和 getResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)方法。

  同步事件需要实现[IDebugEngine2：：：继续从同步事件](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)方法。

  要编写字符串样式输出，必须实现[IDebugStringEvent2：：getString](../../extensibility/debugger/reference/idebugoutputstringevent2-getstring.md)方法。

## <a name="see-also"></a>请参阅
- [执行控制和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)
