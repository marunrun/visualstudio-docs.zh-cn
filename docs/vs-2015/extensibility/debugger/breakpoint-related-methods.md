---
title: 与断点相关的方法 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68146439"
---
# <a name="breakpoint-related-methods"></a>断点相关的方法
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

调试引擎 (DE) 必须支持断点设置。 Visual Studio 调试支持以下类型的断点：  
  
- Bound  
  
     通过 UI 请求并成功绑定到指定的代码位置  
  
- 挂起  
  
     通过 UI 请求，但尚未绑定到实际说明  
  
## <a name="discussion"></a>讨论 (Discussion)  
 例如，如果尚未加载说明，则会发生挂起的断点。 当加载代码时，挂起的断点尝试绑定到指定位置的代码，即在代码中插入中断指令。 事件将发送到会话调试管理器 (SDM) ，以指示成功绑定或通知存在绑定错误。  
  
 挂起的断点还管理其自己的相应绑定断点的内部列表。 一个挂起的断点可能导致在代码中插入多个断点。 Visual Studio 调试 UI 显示挂起断点及其对应绑定断点的树状视图。  
  
 创建和使用挂起的断点需要实现 [IDebugEngine2：： CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) 方法以及以下 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) 接口方法。  
  
|方法|说明|  
|------------|-----------------|  
|[CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|确定指定的挂起断点是否可以绑定到代码位置。|  
|[绑定](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|将指定的挂起断点绑定到一个或多个代码位置。|  
|[GetState](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|获取挂起断点的状态。|  
|[GetBreakpointRequest](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|获取用于创建挂起断点的断点请求。|  
|[启用](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|切换挂起断点的已启用状态。|  
|[EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|枚举从挂起断点绑定的所有断点。|  
|[EnumErrorBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|枚举由挂起断点生成的所有错误断点。|  
|[删除](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|删除挂起的断点以及从该断点绑定的所有断点。|  
  
 若要枚举绑定的断点和错误断点，必须实现 [IEnumDebugBoundBreakpoints2](../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md) 和 [IEnumDebugErrorBreakpoints2](../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)的所有方法。  
  
 绑定到代码位置的挂起断点需要实现以下 [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) 方法。  
  
|方法|说明|  
|------------|-----------------|  
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)|获取包含断点的挂起断点。|  
|[GetState](../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)|获取绑定断点的状态。|  
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)|获取描述断点的断点解析。|  
|[启用](../../extensibility/debugger/reference/idebugboundbreakpoint2-enable.md)|启用或禁用断点。|  
|[删除](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)|删除绑定断点。|  
  
 解析和请求信息需要实现以下 [IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md) 方法。  
  
|方法|说明|  
|------------|-----------------|  
|[GetBreakpointType](../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)|获取由解析表示的断点类型。|  
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)|获取描述断点的断点解析信息。|  
  
 在绑定过程中可能出现的错误的解决方法要求实现以下 [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) 方法。  
  
|方法|说明|  
|------------|-----------------|  
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)|获取包含错误断点的挂起断点。|  
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)|获取描述错误断点的断点错误解析。|  
  
 在绑定过程中可能出现的错误的解决方法还需要 [IDebugErrorBreakpointResolution2](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)的以下方法。  
  
|方法|说明|  
|------------|-----------------|  
|[GetBreakpointType](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getbreakpointtype.md)|获取断点的类型。|  
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)|获取断点的解析信息。|  
  
 在断点处查看源代码需要实现 [IDebugStackFrame2：： GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) 和/或 [IDebugStackFrame2：： GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)方法的方法。  
  
## <a name="see-also"></a>另请参阅  
 [执行控件和状态计算](../../extensibility/debugger/execution-control-and-state-evaluation.md)
