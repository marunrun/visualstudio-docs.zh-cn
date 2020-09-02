---
title: IDebugStackFrame3 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugStackFrame3
helpviewer_keywords:
- IDebugStackFrame3 interface
ms.assetid: 39af2f57-0a01-42b8-b093-b7fbc61e2909
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d63d4dcd6e3b7a3b81504b485ee710779cef3c13
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65688538"
---
# <a name="idebugstackframe3"></a>IDebugStackFrame3
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口扩展 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) 以处理被截获的异常。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugStackFrame3 : IDebugStackFrame2  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 调试引擎 (DE) 在实现 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) 接口的对象上实现此接口，以支持截获的异常。  
  
## <a name="notes-for-callers"></a>调用方说明  
 在接口上调用 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) `IDebugStackFrame2` 以获取此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了从 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)继承的方法之外，还 `IDebugStackFrame3` 公开以下方法。  
  
|方法|说明|  
|------------|-----------------|  
|[InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)|在任何常规异常处理之前处理当前堆栈帧的异常。|  
|[GetUnwindCodeContext](../../../extensibility/debugger/reference/idebugstackframe3-getunwindcodecontext.md)|如果发生堆栈展开，则返回代码上下文。|  
  
## <a name="remarks"></a>备注  
 截获的异常表示在运行时调用任何常规异常处理例程之前，调试器可以处理异常。 截获异常实质上意味着使运行时假设存在异常处理程序，即使没有这样的处理程序。  
  
 [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md) 在所有常规异常回调事件期间调用 (唯一的例外情况是，如果要调试混合模式代码 (托管和非托管代码) ，在这种情况下，在最后一次回调) 期间无法截获异常。 如果未实现 DE `IDebugStackFrame3` ，或 de 从 IDebugStackFrame3：： `InterceptCurrentException` (（如 `E_NOTIMPL`) ）返回错误，则调试器将正常处理异常。  
  
 通过截获异常，调试器可以允许用户对正在调试的程序的状态进行更改，然后在引发异常的点继续执行。  
  
> [!NOTE]
> 仅在托管代码中允许截获的异常，即在运行于公共语言运行时 (CLR) 下的程序中。  
  
 调试引擎指示它支持截获异常，方法是在运行时通过使用函数将 "metricExceptions" 设置为值 1 `SetMetric` 。 有关详细信息，请参阅 [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)   
 [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
