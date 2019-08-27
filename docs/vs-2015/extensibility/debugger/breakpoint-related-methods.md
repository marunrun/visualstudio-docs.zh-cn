---
title: 断点相关的方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], breakpoint methods
- breakpoints, methods
ms.assetid: a6f77bf0-bf81-443f-8683-5f12075bbe10
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 47ba1529521fdce042512a38d32ad2ca2eb3cb82
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68146439"
---
# <a name="breakpoint-related-methods"></a>断点相关的方法
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

调试引擎 (DE) 必须支持的设置的断点。 Visual Studio 调试支持以下类型的断点：  
  
- 绑定  
  
     通过用户界面请求和成功绑定到指定的代码位置  
  
- 挂起  
  
     通过 UI 但尚未绑定到实际说明请求  
  
## <a name="discussion"></a>讨论  
 例如，说明尚未加载时发生挂起断点。 代码加载时，挂起断点 try，它是绑定到代码中的规定的位置，以在代码中插入中断的说明。 事件发送到会话调试管理器 (SDM) 以指示成功绑定或通知未绑定错误。  
  
 挂起断点还管理自己的相应绑定断点的内部列表。 有一个挂起的断点会导致很多断点插入代码中。 在 Visual Studio 调试用户界面显示了挂起断点的树视图和其对应的绑定断点。  
  
 创建和使用挂起断点需要实施[IDebugEngine2::CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)方法，以及下列方法之一[IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)接口。  
  
|方法|描述|  
|------------|-----------------|  
|[CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|确定指定挂起断点可以将绑定到代码位置。|  
|[Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|绑定指定挂起断点到一个或多个代码位置。|  
|[GetState](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|获取挂起断点的状态。|  
|[GetBreakpointRequest](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|获取用于创建挂起断点的断点请求。|  
|[Enable](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|切换挂起断点的启用的状态。|  
|[EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|枚举绑定从挂起断点的所有断点。|  
|[EnumErrorBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|枚举导致的挂起断点的所有错误断点。|  
|[删除](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|删除挂起断点和从该绑定的所有断点。|  
  
 若要枚举的绑定的断点和错误断点，必须实现的所有方法[IEnumDebugBoundBreakpoints2](../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)以及[IEnumDebugErrorBreakpoints2](../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)。  
  
 挂起断点绑定到代码位置需要实现以下[IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)方法。  
  
|方法|描述|  
|------------|-----------------|  
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)|获取包含断点的挂起断点。|  
|[GetState](../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)|获取绑定断点的状态。|  
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)|获取描述断点的断点解决方法。|  
|[Enable](../../extensibility/debugger/reference/idebugboundbreakpoint2-enable.md)|启用或禁用断点。|  
|[删除](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)|删除绑定的断点。|  
  
 解决方法和请求信息需要实现以下[IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md)方法。  
  
|方法|描述|  
|------------|-----------------|  
|[GetBreakpointType](../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)|获取断点表示解析的类型。|  
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)|获取描述断点的断点解决方法信息。|  
  
 绑定过程中可能发生的错误的解决方法需要实现以下[IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)方法。  
  
|方法|描述|  
|------------|-----------------|  
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)|获取包含错误断点挂起断点。|  
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)|获取描述错误断点断点错误解决方法。|  
  
 绑定过程中可能发生的错误的解决方法还需要的以下方法[IDebugErrorBreakpointResolution2](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)。  
  
|方法|描述|  
|------------|-----------------|  
|[GetBreakpointType](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getbreakpointtype.md)|获取断点的类型。|  
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)|获取断点的解决方法信息。|  
  
 查看在断点处的源代码要求您实现的方法[IDebugStackFrame2::GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)和/或方法的[IDebugStackFrame2::GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)。  
  
## <a name="see-also"></a>请参阅  
 [执行控件和状态计算](../../extensibility/debugger/execution-control-and-state-evaluation.md)
