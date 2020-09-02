---
title: IDebugThread2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugThread2
helpviewer_keywords:
- IDebugThread2 interface
ms.assetid: 221b4b1b-4a26-466e-bc29-5eff800fab13
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cabc32d33b1d68b96ae074a8bceac0f759b67447
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152938"
---
# <a name="idebugthread2"></a>IDebugThread2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示在程序中运行的线程。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugThread2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 调试引擎 (DE) 实现此接口，以在单个程序中表示执行线程。  
  
## <a name="notes-for-callers"></a>调用方说明  
 调用 [GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md) 可获取表示当前活动线程的此接口。  
  
 此接口还用于创建断点请求 (参阅 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)) 。  
  
 解析绑定或错误断点时也会返回此接口 (参阅 [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) 和 [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)) 。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugThread2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)|检索此线程的堆栈帧的列表。|  
|[GetName](../../../extensibility/debugger/reference/idebugthread2-getname.md)|获取线程的名称。|  
|[SetThreadName](../../../extensibility/debugger/reference/idebugthread2-setthreadname.md)|设置线程的名称。|  
|[GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)|获取线程正在其中运行的程序。|  
|[CanSetNextStatement](../../../extensibility/debugger/reference/idebugthread2-cansetnextstatement.md)|确定是否可以将下一条语句设置为给定的堆栈帧和代码上下文。|  
|[SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)|将下一条语句设置为给定的堆栈帧和代码上下文。|  
|[GetThreadId](../../../extensibility/debugger/reference/idebugthread2-getthreadid.md)|获取系统线程标识符。|  
|[挂起](../../../extensibility/debugger/reference/idebugthread2-suspend.md)|挂起线程。|  
|[恢复](../../../extensibility/debugger/reference/idebugthread2-resume.md)|恢复线程。|  
|[GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)|获取描述线程的属性。|  
|[GetLogicalThread](../../../extensibility/debugger/reference/idebugthread2-getlogicalthread.md)|获取与此物理线程关联的逻辑线程。|  
  
## <a name="remarks"></a>备注  
 由于单个物理线程可以在多个程序中运行，因此多个程序中的多个 `IDebugThread2` 可以表示同一个物理线程。  
  
 发生断点或异常时，通过调用 [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)发送事件。 此方法的参数之一是 `IDebugThread2` 表示当前线程的接口。 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) 用于获取当前堆栈帧的 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) 接口。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [引发](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)   
 [GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)   
 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)   
 [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)   
 [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
