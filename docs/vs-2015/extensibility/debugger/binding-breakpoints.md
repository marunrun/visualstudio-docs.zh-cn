---
title: 绑定断点 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, binding
ms.assetid: 70737387-c52f-4dae-8865-77d4b203bf25
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fc7f68093432c96d496921ea593b6e936bad8302
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68147964"
---
# <a name="binding-breakpoints"></a>绑定断点
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

如果用户设置一个断点，可能是通过按 F9，IDE 表述请求并提示调试会话才能创建断点。  
  
## <a name="setting-a-breakpoint"></a>设置断点  
 设置断点是一个两步过程，因为代码或数据受影响的断点可能尚不可用。 首先，必须描述断点，，然后，在代码或数据可用，它必须绑定到该代码或数据，按如下所示：  
  
1. 断点请求从相关的调试引擎 (DEs)，然后绑定到断点的代码或数据变得可用。  
  
2. 断点请求发送到调试会话，将其发送到所有相关的 DEs。 选择来处理断点任何 DE 创建相应的挂起断点。  
  
3. 调试会话收集的挂起断点，并将其返回给调试包 （Visual Studio 的调试组件）。  
  
4. 调试包会提示在调试会话将挂起断点绑定到代码或数据。 调试会话将此请求发送到所有相关的 DEs。  
  
5. 如果 DE 能够将断点绑定，它将发送一个断点绑定事件返回到调试会话。 如果没有，而是发送断点错误事件。  
  
## <a name="pending-breakpoints"></a>挂起断点  
 挂起断点可以绑定到多个代码位置。 例如，线的源代码C++模板可绑定到从模板生成的每个代码序列。 调试会话可以使用断点绑定的事件以枚举在发送该事件的时间绑定到断点的代码上下文。 可以从更高版本，绑定多个代码上下文，因此 DE 可能会发送多个断点绑定为每个绑定请求的事件。 但是，DE 应发送每个绑定请求只能有一个断点错误事件。  
  
## <a name="implementation"></a>实现  
 调试包，以编程方式调用会话调试管理器 (SDM) 并为其提供[IDebugBreakpointRequest2](../../extensibility/debugger/reference/idebugbreakpointrequest2.md)包装的接口[BP_REQUEST_INFO](../../extensibility/debugger/reference/bp-request-info.md)结构，它描述若要设置的断点。 尽管断点可以为多种形式，但它们最终解析代码或数据上下文。  
  
 SDM 将对每个相关 DE 的此调用传递通过调用其[CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)方法。 如果 DE 选择来处理断点，它创建并返回[IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)接口。 SDM 收集这些接口，并将其传递回调试程序包作为单个`IDebugPendingBreakpoint2`接口。  
  
 到目前为止，已不生成任何事件。  
  
 调试包然后尝试将挂起断点的代码或数据绑定通过调用[绑定](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)，这由 DE 实现。  
  
 如果绑定断点，将发送 DE [IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)调试包的事件接口。 此接口可枚举所有代码上下文 （或单个数据上下文） 通过调用绑定到断点调试包用[EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)，这会返回一个或多个[IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)接口。 [GetBreakpointResolution](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)接口返回[IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md)接口，并且[GetResolutionInfo](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)返回[BP_RESOLUTION_INFO](../../extensibility/debugger/reference/bp-resolution-info.md)包含代码或数据上下文的并集。  
  
 如果设备不能将断点绑定，则会发送单个[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)调试包的事件接口。 调试包检索的错误类型 （错误或警告） 和信息性消息，通过调用[GetErrorBreakpoint](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)后, 跟[GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)和[GetResolutionInfo](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)。 这将返回[BP_ERROR_RESOLUTION_INFO](../../extensibility/debugger/reference/bp-error-resolution-info.md)结构，其中包含的错误类型和消息。  
  
 如果 DE 处理断点，但不能将其绑定，它将返回类型的错误`BPET_TYPE_ERROR`。 调试包响应通过显示错误对话框，并在 IDE 将放置在左侧的源代码行的断点标志符号为感叹号标志符号。  
  
 如果 DE 处理断点，而不能绑定，但某些其他 DE 可能将其绑定，则会返回警告。 通过将放置在左侧的源代码行的断点标志符号的问题标志符号，IDE 响应。  
  
## <a name="see-also"></a>请参阅  
 [调试任务](../../extensibility/debugger/debugging-tasks.md)
