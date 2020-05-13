---
title: 断点相关方法 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], breakpoint methods
- breakpoints, methods
ms.assetid: a6f77bf0-bf81-443f-8683-5f12075bbe10
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c72ec63e500ac86a4a5bd66a2956fe0fb06c8834
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739205"
---
# <a name="breakpoint-related-methods"></a>与断点相关的方法
调试引擎 （DE） 必须支持断点设置。 Visual Studio 调试支持以下类型的断点：

- Bound

     通过 UI 请求并成功绑定到指定的代码位置

- 挂起的

     通过 UI 请求但尚未绑定到实际说明

## <a name="discussion"></a>讨论区
 例如，当指令尚未加载时，将发生挂起的断点。 加载代码时，挂起的断点尝试绑定到指定位置的代码，即在代码中插入中断指令。 事件将发送到会话调试管理器 （SDM）， 以指示成功的绑定或通知存在绑定错误。

 挂起的断点还管理其自己的相应绑定断点的内部列表。 一个挂起的断点可能导致在代码中插入许多断点。 Visual Studio 调试 UI 显示挂起断点的树视图及其相应的绑定断点。

 创建和使用挂起的断点需要实现[IDebugEngine2：：：creatependingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)方法以及[以下 IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)接口的方法。

|方法|描述|
|------------|-----------------|
|[CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|确定指定的挂起断点是否可以绑定到代码位置。|
|[绑定](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|将指定的挂起断点绑定到一个或多个代码位置。|
|[获取状态](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|获取挂起断点的状态。|
|[GetBreakpointRequest](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|获取用于创建挂起断点的断点请求。|
|[启用](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|切换挂起断点的启用状态。|
|[EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|枚举从挂起的断点绑定的所有断点。|
|[EnumErrorBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|枚举来自挂起断点的所有错误断点。|
|[删除](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|删除挂起的断点和所有断点。|

 要枚举绑定断点和错误断点，必须实现[IEnumDebugBoundBreakpoints2](../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)和[IEnumDebugErrorBreakpoints2](../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)的所有方法。

 绑定到代码位置的挂起断点需要实现以下[IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)方法。

|方法|描述|
|------------|-----------------|
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)|获取包含断点的挂起断点。|
|[获取状态](../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)|获取绑定断点的状态。|
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)|获取描述断点的断点分辨率。|
|[启用](../../extensibility/debugger/reference/idebugboundbreakpoint2-enable.md)|启用或禁用断点。|
|[删除](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)|删除绑定断点。|

 解析和请求信息需要实现以下[IDebugBreakpoint 决议2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md)方法。

|方法|描述|
|------------|-----------------|
|[GetBreakpointType](../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)|获取由分辨率表示的断点的类型。|
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)|获取描述断点的断点分辨率信息。|

 解决绑定期间可能发生的错误需要实现以下[IDebugErrorBreakpointpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)方法。

|方法|描述|
|------------|-----------------|
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)|获取包含错误断点的挂起断点。|
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)|获取描述错误断点的断点错误分辨率。|

 解决绑定期间可能发生的错误还需要以下方法的[IDebugErrorBreakpoint决议2](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)。

|方法|描述|
|------------|-----------------|
|[GetBreakpointType](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getbreakpointtype.md)|获取断点的类型。|
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)|获取断点的分辨率信息。|

 在断点处查看源代码需要实现[IDebugStackFrame2：：：：获取文档上下文](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)和/或[IDebugStackFrame2：：：获取代码上下文](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)的方法。

## <a name="see-also"></a>请参阅
- [执行控制和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)
