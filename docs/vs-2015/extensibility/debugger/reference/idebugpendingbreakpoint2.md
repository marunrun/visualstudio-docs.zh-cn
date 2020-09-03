---
title: IDebugPendingBreakpoint2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2
helpviewer_keywords:
- IDebugPendingBreakpoint2 interface
ms.assetid: d416b095-917e-475e-b796-ec0a03ffb8da
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1238fcbce22db3f3bc3e32019aac886c79d0c114
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68201026"
---
# <a name="idebugpendingbreakpoint2"></a>IDebugPendingBreakpoint2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示已准备好绑定到代码位置的断点。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugPendingBreakpoint2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 调试引擎 (DE) 实现此接口作为其对断点的支持的一部分。  
  
## <a name="notes-for-callers"></a>调用方说明  
 对 [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) 的调用将从 [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md) 接口创建挂起断点。 [绑定](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)调用会创建一个 `IDebugBreakpoint2` 接口，该接口表示程序中的绑定断点。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugPendingBreakpoint2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|确定此挂起断点是否可以绑定到代码位置。|  
|[绑定](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|将此挂起断点绑定到一个或多个代码位置。|  
|[GetState](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|获取此挂起断点的状态。|  
|[GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|获取用于创建此挂起断点的断点请求。|  
|[Virtualize](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)|切换此挂起断点的虚拟化状态。|  
|[启用](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|切换此挂起断点的已启用状态。|  
|[SetCondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md)|设置或更改与此挂起断点关联的条件。|  
|[SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)|设置或更改与此挂起断点关联的传递计数。|  
|[EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|枚举从此挂起断点绑定的所有断点。|  
|[EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|枚举此挂起断点导致的所有错误断点。|  
|[删除](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|删除此挂起断点及其绑定的所有断点。|  
  
## <a name="remarks"></a>备注  
 `IDebugPendingBreakpoint2` 可以被视为将断点绑定到可应用于一个或多个程序的代码所需的所有必需信息的提供程序。  
  
 挂起的断点可能会生成多个绑定断点。 例如，c + + 样式模板中的断点可以为该模板的每个唯一实例生成一个绑定断点。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)   
 [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)   
 [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)   
 [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)
