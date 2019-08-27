---
title: IDebugStackFrame3::InterceptCurrentException | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugStackFrame3::InterceptCurrentException
helpviewer_keywords:
- IDebugStackFrame3::InterceptCurrentException
ms.assetid: 116c7324-7645-4c15-b484-7a5cdd065ef5
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 42472690431d48a9baafbb0abee27c1a07d24fcd
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63428692"
---
# <a name="idebugstackframe3interceptcurrentexception"></a>IDebugStackFrame3::InterceptCurrentException
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

当它想要截获的当前异常时由当前堆栈帧上的调试器调用。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT InterceptCurrentException(  
   INTERCEPT_EXCEPTION_ACTION dwFlags,  
   UINT64*                    pqwCookie  
);  
```  
  
```csharp  
int InterceptCurrentException(  
   uint dwFlags,   
   out  ulong pqwCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwFlags`  
 [in]指定不同的操作。 目前，仅[INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md)值`IEA_INTERCEPT`支持，并且必须指定。  
  
 `pqwCookie`  
 [out]标识特定异常的唯一值。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 S_OK;否则，返回错误代码。  
  
 以下是最常见的错误返回。  
  
|Error|描述|  
|-----------|-----------------|  
|`E_EXCEPTION_CANNOT_BE_INTERCEPTED`|不能截获当前异常。|  
|`E_EXCEPTION_CANNOT_UNWIND_ABOVE_CALLBACK`|当前的执行帧未尚未搜索处理程序。|  
|`E_INTERCEPT_CURRENT_EXCEPTION_NOT_SUPPORTED`|此框架不支持此方法。|  
  
## <a name="remarks"></a>备注  
 引发异常时，调试器在异常处理过程期间者控制了从运行时的关键点。 在这些关键时间点，调试器就可以要求当前堆栈帧帧想要截获的异常。 这样一来，已截获的异常是实质上是动态在异常处理程序的堆栈帧，即使该堆栈帧不具有异常处理程序 （例如，try/catch 块的程序代码中）。  
  
 当调试器想要知道是否拦截异常时，它在当前堆栈帧对象上调用此方法。 此方法负责处理异常的所有详细信息。 如果[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)未实现接口或`InterceptStackException`方法会返回任何错误，则调试器会继续正常处理该异常。  
  
> [!NOTE]
> 异常会被截取只能在托管代码中，它是正在调试的程序在运行时的.NET 下运行时。 当然，第三方语言实现者可以实现`InterceptStackException`中选择性地他们自己的调试引擎。  
  
 拦截完成后[IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)发出信号。  
  
## <a name="see-also"></a>请参阅  
 [IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)   
 [INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md)   
 [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)
