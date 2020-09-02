---
title: IEnumDebugBoundBreakpoints2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugBoundBreakpoints2
helpviewer_keywords:
- IEnumDebugBoundBreakpoints2
ms.assetid: ea03e7e1-28d6-40b7-8097-bbb61d3b7caa
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6e738d4714072c36628046583104e2d47bcc563e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62551861"
---
# <a name="ienumdebugboundbreakpoints2"></a>IEnumDebugBoundBreakpoints2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口枚举与挂起断点或断点绑定事件关联的绑定断点。  
  
## <a name="syntax"></a>语法  
  
```  
IEnumDebugBoundBreakpoints2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 调试引擎 (DE) 实现此接口作为其对断点的支持的一部分。 如果支持断点，则必须实现此接口。  
  
## <a name="notes-for-callers"></a>调用方说明  
 Visual Studio 调用：  
  
- [EnumBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointevent2-enumbreakpoints.md) 获取表示所有已触发断点列表的此接口。  
  
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md) 获取表示所有绑定断点列表的此接口。  
  
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md) 获取此接口，该接口表示绑定到该挂起断点的所有断点的列表。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IEnumDebugBoundBreakpoints2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[下一页](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-next.md)|检索枚举序列中指定数目的绑定断点。|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-skip.md)|跳过枚举序列中指定数目的绑定断点。|  
|[重置](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-reset.md)|将枚举序列重置到开始处。|  
|[克隆](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-getcount.md)|获取枚举器中绑定断点的数目。|  
  
## <a name="remarks"></a>备注  
 Visual Studio 使用此接口所表示的绑定断点更新 IDE 中断点的显示。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)   
 [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)   
 [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)
