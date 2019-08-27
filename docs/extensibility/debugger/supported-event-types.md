---
title: 支持的事件类型 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], supported events
ms.assetid: a3c0386d-551e-4734-9a0c-368d1c2e6671
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9c4ee45e1a3a7efeb990fcb6f9073420a99dbe7c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351094"
---
# <a name="supported-event-types"></a>支持的事件类型
Visual Studio 调试当前支持以下事件类型：

- 异步事件

   通知会话调试管理器 (SDM) 和正在调试的应用程序的状态将更改的 IDE。 SDM 和 IDE 的閒旅遊处理这些事件。 处理事件后，会不发送到调试引擎 (DE) 任何回复。 [IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md)并[IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md)接口是异步事件的示例。

- 同步事件

   通知 SDM 和正在调试的应用程序的状态将更改的 IDE。 这些事件和异步事件的唯一区别在于，通过发送答复[ContinueFromSynchronousEvent](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)方法。

   发送同步事件是很有用，如果您需要在 DE 以继续处理后 IDE 接收并处理该事件。

- 同步的停止事件，或停止事件

   通知 SDM 和 IDE 正在调试的应用程序已停止执行代码。 如果要将停止事件发送方法[事件](../../extensibility/debugger/reference/idebugeventcallback2-event.md)，则[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)参数是必需的。 正在停止事件是通过调用以下方法之一 （续）：

  - [Execute](../../extensibility/debugger/reference/idebugprogram2-execute.md)

  - [Step](../../extensibility/debugger/reference/idebugprogram2-step.md)

  - [Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)

    接口[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)并[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)是停止事件的示例。

  > [!NOTE]
  > 不支持异步停止事件。 它是错误发送异步停止事件。

## <a name="discussion"></a>讨论
 事件的实际实现取决于你 DE 设计。 发送每个事件的类型是由设计 DE 时设置其属性确定的。 例如，可能会发送一个 DE [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)作为异步事件，而另一个可能会将其作为停止事件。

 下表指定哪些程序和线程的参数是必需的事件，以及事件类型。 任何事件可以是同步的。 不需要是同步的任何事件。

> [!NOTE]
> [IDebugEngine2](../../extensibility/debugger/reference/idebugengine2.md)接口是必需的所有事件。

|Event|IDebugProgram2|IDebugThread2|停止事件|
|-----------|--------------------|-------------------|---------------------|
|[IDebugActivateDocumentEvent2](../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|允许，但不是必需|允许，但不是必需|否|
|[IDebugBreakEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md)|必需|必需|是|
|[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|允许，但不是必需|允许，但不是必需|否|
|[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|允许，但不是必需|允许，但不是必需|否|
|[IDebugBreakpointUnboundEvent2](../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|允许，但不是必需|允许，但不是必需|否|
|[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)|必需|必需|是|
|[IDebugCanStopEvent2](../../extensibility/debugger/reference/idebugcanstopevent2.md)|必需|必需|否|
|[IDebugDocumentTextEvents2](../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|不允许|不允许|否|
|[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)|不允许|不允许|否|
|[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)|必需|必需|是|
|[IDebugErrorEvent2](../../extensibility/debugger/reference/idebugerrorevent2.md)|允许，但不是必需|允许，但不是必需|可以|
|[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)|必需|必需|是|
|[IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|允许，但不是必需|允许，但不是必需|可以|
|[IDebugInterceptExceptionCompleteEvent2](../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)|必需|必需|是|
|[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)|必需|必需|是|
|[IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md)|允许，但不是必需|允许，但不是必需|可以|
|[IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|必需|允许，但不是必需|否|
|[IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md)|允许，但不是必需|允许，但不是必需|否|
|[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|必需|允许，但不是必需|否|
|[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|必需|允许，但不是必需|否|
|[IDebugPropertyCreateEvent2](../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|必需|允许，但不是必需|否|
|[IDebugPropertyDestroyEvent2](../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|必需|允许，但不是必需|否|
|[IDebugReturnValueEvent2](../../extensibility/debugger/reference/idebugreturnvalueevent2.md)|允许，但不是必需|允许，但不是必需|否|
|IDebugStopCompleteEvent2|必需|必需|是|
|[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)|必需|必需|是|
|[IDebugSymbolSearchEvent2](../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)|允许，但不是必需|允许，但不是必需|否|
|[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|必需|必需|否|
|[IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|必需|必需|否|
|[IDebugThreadNameChangedEvent2](../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|允许，但不是必需|允许，但不是必需|否|

## <a name="see-also"></a>请参阅
- [发送事件](../../extensibility/debugger/sending-events.md)