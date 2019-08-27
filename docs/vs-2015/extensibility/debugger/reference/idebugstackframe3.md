---
title: IDebugStackFrame3 | Microsoft Docs
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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65688538"
---
# <a name="idebugstackframe3"></a>IDebugStackFrame3
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口扩展[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)来处理已截获的异常。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugStackFrame3 : IDebugStackFrame2  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 调试引擎 (DE) 实现此接口上实现的相同对象[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)接口以支持已截获的异常。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 调用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)上`IDebugStackFrame2`接口，以获得此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了继承的方法之外[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)，`IDebugStackFrame3`公开以下方法。  
  
|方法|描述|  
|------------|-----------------|  
|[InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)|处理当前堆栈帧之前任何常规异常处理的异常。|  
|[GetUnwindCodeContext](../../../extensibility/debugger/reference/idebugstackframe3-getunwindcodecontext.md)|出现堆栈展开时，返回代码上下文。|  
  
## <a name="remarks"></a>备注  
 已截获的异常意味着运行时在调用任何常规异常处理例程之前调试程序，可以处理异常。 实质上截获异常意味着使假设是存在，即使没有异常处理程序的运行的时间。  
  
 [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)在普通的异常的所有回调事件期间调用 (唯一的例外情况是如果你正在调试混合模式代码 （托管和非托管代码），在这种情况下不能在拦截异常最后一个回调）。 如果未实现 DE `IDebugStackFrame3`，或 DE 从 IDebugStackFrame3 返回错误::`InterceptCurrentException` (如`E_NOTIMPL`)，则调试器将正常处理此异常。  
  
 通过截获异常，调试器可以允许用户对正在调试的程序的状态进行更改，然后继续执行在引发异常的点。  
  
> [!NOTE]
> 已截获的异常只允许出现在托管代码中，即，在程序运行在公共语言运行时 (CLR) 中。  
  
 调试引擎，它支持通过设置"metricExceptions"截取异常为值 1 在运行时通过使用指示`SetMetric`函数。 有关详细信息，请参阅[以便进行调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)   
 [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
