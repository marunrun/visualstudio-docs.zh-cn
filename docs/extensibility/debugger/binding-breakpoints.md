---
title: 绑定断点 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, binding
ms.assetid: 70737387-c52f-4dae-8865-77d4b203bf25
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 680cff398a43d1ebe9ccf061ad42781500c7cf01
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739228"
---
# <a name="bind-breakpoints"></a>绑定断点
如果用户设置断点（可能通过按**F9），IDE**将制定请求并提示调试会话创建断点。

## <a name="set-a-breakpoint"></a>设置断点
 设置断点是一个两步过程，因为受断点影响的代码或数据可能尚未可用。 首先，必须描述断点，然后，当代码或数据可用时，必须将其绑定到该代码或数据，如下所示：

1. 从相关调试引擎 （DEs） 请求断点，然后断点在可用时绑定到代码或数据。

2. 断点请求发送到调试会话，调试会话将其发送到所有相关的 D。 任何选择处理断点的 DE 都会创建相应的挂起断点。

3. 调试会话收集挂起的断点并将其发送回调试包（Visual Studio 的调试组件）。

4. 调试包提示调试会话将挂起的断点绑定到代码或数据。 调试会话将此请求发送到所有相关的 D。

5. 如果 DE 能够绑定断点，它将一个断点绑定事件发送回调试会话。 如果没有，它将发送断点错误事件。

## <a name="pending-breakpoints"></a>挂起的断点
 挂起的断点可以绑定到多个代码位置。 例如，C++模板的一行源代码可以绑定到从模板生成的每个代码序列。 调试会话可以使用断点绑定事件枚举在发送事件时绑定到断点的代码上下文。 以后可以绑定更多代码上下文，因此 DE 可能会为每个绑定请求发送多个断点绑定事件。 但是，DE 应仅发送每个绑定请求的一个断点错误事件。

## <a name="implementation"></a>实现
 在编程上，调试包调用会话调试管理器 （SDM），并给它一个[IDebugBreakpointRequest2](../../extensibility/debugger/reference/idebugbreakpointrequest2.md)接口，该接口包装[BP_REQUEST_INFO](../../extensibility/debugger/reference/bp-request-info.md)结构，该结构描述了要设置的断点。 尽管断点可以是多种形式，但它们最终解析为代码或数据上下文。

 SDM 通过调用其[CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)方法将此调用传递给每个相关的 DE。 如果 DE 选择处理断点，它将创建并返回[IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)接口。 SDM 收集这些接口并将其作为单个`IDebugPendingBreakpoint2`接口传回调试包。

 到目前为止，尚未生成任何事件。

 然后，调试包尝试通过调用 DE 实现的[Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)将挂起的断点绑定到代码或数据。

 如果断点绑定，DE 会向调试包发送[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)事件接口。 调试包使用此接口通过调用[EnumBoundBreakpoint](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)来枚举绑定到断点的的所有代码上下文（或单个数据上下文），该接口返回一个或多个[IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)接口。 [GetBreakpoint 解析](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)接口返回[IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md)接口[，GetResolutionInfo](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)返回包含代码或数据上下文[BP_RESOLUTION_INFO](../../extensibility/debugger/reference/bp-resolution-info.md)联合。

 如果 DE 无法绑定断点，它将向调试包发送单个[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)事件接口。 调试包通过调用[GetErrorBreakpoint](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)检索错误类型（错误或警告）和信息性消息，然后是[GetBreakpoint 解析](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)和[Get解析信息](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)。 这将返回包含错误类型和消息[BP_ERROR_RESOLUTION_INFO](../../extensibility/debugger/reference/bp-error-resolution-info.md)结构。

 如果 DE 处理断点但无法绑定它，它将返回类型 错误`BPET_TYPE_ERROR`。 调试包通过显示错误对话框进行响应，IDE 在源代码行左侧的断点字形内放置一个感叹号。

 如果 DE 处理断点，无法绑定它，但其他 DE 可能会绑定它，则返回警告。 IDE 通过在源代码行左侧的断点字形内放置一个问题字形来响应。

## <a name="see-also"></a>请参阅
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
