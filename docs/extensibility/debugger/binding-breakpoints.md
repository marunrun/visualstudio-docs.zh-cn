---
title: 绑定断点 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- breakpoints, binding
ms.assetid: 70737387-c52f-4dae-8865-77d4b203bf25
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e839b6e0e7967c4802bee5617da3334c5d4033c5
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903229"
---
# <a name="bind-breakpoints"></a>绑定断点
如果用户通过按**F9**设置断点，则 IDE 会形成请求，并提示调试会话创建断点。

## <a name="set-a-breakpoint"></a>设置断点
 设置断点的过程分为两个步骤，因为受断点影响的代码或数据可能尚未提供。 首先，必须描述断点，然后在代码或数据可用时，必须将其绑定到该代码或数据，如下所示：

1. 将从相关的调试引擎（DEs）请求断点，然后将断点绑定到可用的代码或数据。

2. 将断点请求发送到调试会话，并将其发送到所有相关的 DEs。 选择处理断点的任何 DE 都将创建一个相应的挂起断点。

3. 调试会话收集挂起的断点，并将其发送回调试包（Visual Studio 的调试组件）。

4. 调试包将提示调试会话将挂起断点绑定到代码或数据。 调试会话将此请求发送到所有相关的 DEs。

5. 如果 DE 能够绑定断点，则会将断点绑定事件发送回调试会话。 否则，将改为发送断点错误事件。

## <a name="pending-breakpoints"></a>挂起断点
 挂起的断点可以绑定到多个代码位置。 例如，c + + 模板的行代码可绑定到每个从模板生成的代码序列。 调试会话可以使用断点绑定事件枚举在发送事件时绑定到断点的代码上下文。 稍后可以绑定更多的代码上下文，因此，可能会为每个绑定请求发送多个断点绑定事件。 但是，每个绑定请求的 DE 只应发送一个断点错误事件。

## <a name="implementation"></a>实现
 调试包以编程方式调用会话调试管理器（SDM），并为其提供一个包装[BP_REQUEST_INFO](../../extensibility/debugger/reference/bp-request-info.md)结构的[IDebugBreakpointRequest2](../../extensibility/debugger/reference/idebugbreakpointrequest2.md)接口，该接口描述要设置的断点。 尽管断点可以是多种形式，但它们最终解析为代码或数据上下文。

 SDM 通过调用其[CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)方法将此调用传递给每个相关的 DE。 如果取消选择处理断点，则会创建并返回[IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)接口。 SDM 收集这些接口，并将它们作为单个接口传递回调试包 `IDebugPendingBreakpoint2` 。

 到目前为止，未生成任何事件。

 然后，调试包会通过调用由 DE 实现的[bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)，尝试将挂起断点绑定到代码或数据。

 如果绑定了断点，则 DE 会将[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)事件接口发送到调试包。 调试包使用此接口来枚举绑定到断点的所有代码上下文（或单个数据上下文），方法是调用[EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)，后者将返回一个或多个[IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)接口。 [GetBreakpointResolution](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)接口返回[IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md)接口， [GetResolutionInfo](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)返回包含代码或数据上下文的[BP_RESOLUTION_INFO](../../extensibility/debugger/reference/bp-resolution-info.md)联合。

 如果 DE 无法绑定断点，则会向调试包发送单个[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)事件接口。 调试包通过调用[GetErrorBreakpoint](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)来检索错误类型（错误或警告）和信息性消息，后跟[GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)和[GetResolutionInfo](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)。 这会返回包含错误类型和消息的[BP_ERROR_RESOLUTION_INFO](../../extensibility/debugger/reference/bp-error-resolution-info.md)结构。

 如果 DE 处理断点但无法绑定它，则它会返回类型为的错误 `BPET_TYPE_ERROR` 。 调试包通过显示错误对话框进行响应，而 IDE 在源代码行左侧的断点标志符号内放置感叹号标志符号。

 如果 DE 处理断点，则无法绑定它，但其他一些 DE 可能会绑定它，它会返回警告。 IDE 通过将问题标志符号放置在源代码行左侧的断点标志符号中来做出响应。

## <a name="see-also"></a>另请参阅
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
