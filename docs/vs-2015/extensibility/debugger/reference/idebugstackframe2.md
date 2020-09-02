---
title: IDebugStackFrame2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugStackFrame2
helpviewer_keywords:
- IDebugStackFrame2 interface
ms.assetid: bd212a6a-dcc6-4756-a77a-e8dfda38b104
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ae9cad7102fb9a82deb43b2c8820ef52e77deeed
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62546998"
---
# <a name="idebugstackframe2"></a>IDebugStackFrame2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示特定线程中的调用堆栈中的单个堆栈帧。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugStackFrame2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 调试引擎 (DE) 实现此接口以表示堆栈帧。  
  
## <a name="notes-for-callers"></a>调用方说明  
 调用 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) 可检索 [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md) 接口。 [接下来](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)，调用以检索包含接口的[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构 `IDebugStackFrame2` 。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugStackFrame2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|获取此堆栈帧的代码上下文。|  
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|获取此堆栈帧的文档上下文。|  
|[GetName](../../../extensibility/debugger/reference/idebugstackframe2-getname.md)|获取堆栈帧的名称。|  
|[GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)|获取堆栈帧的说明。|  
|[GetPhysicalStackRange](../../../extensibility/debugger/reference/idebugstackframe2-getphysicalstackrange.md)|获取与堆栈帧关联的物理地址范围的依赖于计算机的表示形式。|  
|[GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)|获取用于在堆栈帧和线程的当前上下文中执行表达式计算的计算上下文。|  
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugstackframe2-getlanguageinfo.md)|获取与堆栈帧关联的语言。|  
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)|获取与堆栈帧关联的属性的说明。|  
|[EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)|为堆栈帧属性创建枚举器。|  
|[GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)|获取与堆栈帧关联的线程。|  
  
## <a name="remarks"></a>备注  
 仅当正在调试的程序已在断点处停止时，才会获得此接口 (是由用户设置断点或异常) 导致的。 通过此接口，可以获取表达式上下文来计算表达式、返回寄存器列表，或获取和检查调用堆栈。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
