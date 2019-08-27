---
title: IEnumDebugBoundBreakpoints2 | Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62551861"
---
# <a name="ienumdebugboundbreakpoints2"></a>IEnumDebugBoundBreakpoints2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口枚举与挂起断点关联的绑定的断点或绑定断点的事件。  
  
## <a name="syntax"></a>语法  
  
```  
IEnumDebugBoundBreakpoints2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 调试引擎 (DE) 实现此接口作为断点的支持的一部分。 如果支持断点，则必须实现此接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 Visual Studio 会调用：  
  
- [EnumBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointevent2-enumbreakpoints.md)获取表示已触发的所有断点的列表的此接口。  
  
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)若要获取此界面表示绑定的所有断点的列表。  
  
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)若要获取此界面表示绑定到该挂起断点的所有断点的列表。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IEnumDebugBoundBreakpoints2`。  
  
|方法|描述|  
|------------|-----------------|  
|[下一页](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-next.md)|检索指定的数目的枚举序列中的绑定断点。|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-skip.md)|跳过枚举序列中的绑定断点的指定的数目。|  
|[Reset](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-reset.md)|将枚举序列重置到开头。|  
|[Clone](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-getcount.md)|获取一个枚举器中的绑定断点的数。|  
  
## <a name="remarks"></a>备注  
 Visual Studio 使用此接口由表示的绑定的断点来更新显示在 IDE 中的断点。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)   
 [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)   
 [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)
