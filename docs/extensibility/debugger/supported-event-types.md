---
title: 支持的事件类型 |Microsoft Docs
description: 了解 Visual Studio 调试支持的事件类型，包括异步事件、同步事件和停止事件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], supported events
ms.assetid: a3c0386d-551e-4734-9a0c-368d1c2e6671
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 215256cbbcff45dfa0b85a480f0900e6f8ddfa71
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96996027"
---
# <a name="supported-event-types"></a>支持的事件类型
Visual Studio 调试当前支持以下事件类型：

- 异步事件

   通知会话调试管理器 (SDM) 和 IDE 中正在进行调试的应用程序的状态正在更改。 这些事件是在 SDM 和 IDE 的休闲上处理的。 处理事件后 (DE) ，不会将任何答复发送到调试引擎。 [IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md)和[IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md)接口都是异步事件的示例。

- 同步事件

   通知 SDM 和 IDE 正在更改的应用程序的状态。 这些事件和异步事件的唯一区别是通过 [ContinueFromSynchronousEvent](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md) 方法发送回复。

   如果需要在 IDE 接收并处理事件后继续处理，则发送同步事件很有用。

- 同步停止事件或停止事件

   通知 SDM 和 IDE：正在调试的应用程序已停止执行代码。 通过方法 [事件](../../extensibility/debugger/reference/idebugeventcallback2-event.md)发送停止事件时， [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) 参数是必需的。 通过调用以下方法之一，停止事件会继续：

  - [执行](../../extensibility/debugger/reference/idebugprogram2-execute.md)

  - [步骤](../../extensibility/debugger/reference/idebugprogram2-step.md)

  - [继续](../../extensibility/debugger/reference/idebugprogram2-continue.md)

    接口 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) 和 [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md) 是停止事件的示例。

  > [!NOTE]
  > 不支持异步停止事件。 发送异步停止事件是错误的。

## <a name="discussion"></a>讨论 (Discussion)
 事件的实际实现取决于您的 DE 的设计。 发送的每个事件的类型由其特性确定，这是在设计 DE 时设置的。 例如，一个 DE 可能会以异步事件的形式发送 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) ，而另一个则可能将其作为停止事件发送。

 下表指定了哪些事件以及事件类型需要哪个程序和线程参数。 任何事件都可以是同步的。 无事件需要同步。

> [!NOTE]
> 所有事件都需要 [IDebugEngine2](../../extensibility/debugger/reference/idebugengine2.md) 接口。

|事件|IDebugProgram2|IDebugThread2|停止事件|
|-----------|--------------------|-------------------|---------------------|
|[IDebugActivateDocumentEvent2](../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|允许，但不需要|允许，但不需要|否|
|[IDebugBreakEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md)|必选|必需|是|
|[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|允许，但不需要|允许，但不需要|否|
|[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|允许，但不需要|允许，但不需要|否|
|[IDebugBreakpointUnboundEvent2](../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|允许，但不需要|允许，但不需要|否|
|[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)|必选|必需|是|
|[IDebugCanStopEvent2](../../extensibility/debugger/reference/idebugcanstopevent2.md)|必选|必选|否|
|[IDebugDocumentTextEvents2](../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|不允许|不允许|否|
|[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)|不允许|不允许|否|
|[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)|必选|必需|是|
|[IDebugErrorEvent2](../../extensibility/debugger/reference/idebugerrorevent2.md)|允许，但不需要|允许，但不需要|可以|
|[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)|必选|必需|是|
|[IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|允许，但不需要|允许，但不需要|可以|
|[IDebugInterceptExceptionCompleteEvent2](../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)|必选|必需|是|
|[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)|必选|必需|是|
|[IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md)|允许，但不需要|允许，但不需要|可以|
|[IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|必选|允许，但不需要|否|
|[IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md)|允许，但不需要|允许，但不需要|否|
|[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|必选|允许，但不需要|否|
|[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|必选|允许，但不需要|否|
|[IDebugPropertyCreateEvent2](../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|必选|允许，但不需要|否|
|[IDebugPropertyDestroyEvent2](../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|必选|允许，但不需要|否|
|[IDebugReturnValueEvent2](../../extensibility/debugger/reference/idebugreturnvalueevent2.md)|允许，但不需要|允许，但不需要|否|
|IDebugStopCompleteEvent2|必选|必需|是|
|[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)|必选|必需|是|
|[IDebugSymbolSearchEvent2](../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)|允许，但不需要|允许，但不需要|否|
|[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|必选|必选|否|
|[IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|必选|必选|否|
|[IDebugThreadNameChangedEvent2](../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|允许，但不需要|允许，但不需要|否|

## <a name="see-also"></a>另请参阅
- [发送事件](../../extensibility/debugger/sending-events.md)
