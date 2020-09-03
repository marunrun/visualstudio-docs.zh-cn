---
title: IDebugStackFrame3：： InterceptCurrentException |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame3::InterceptCurrentException
helpviewer_keywords:
- IDebugStackFrame3::InterceptCurrentException
ms.assetid: 116c7324-7645-4c15-b484-7a5cdd065ef5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7debd5323e753c6c5fd1476eac3c062fb63393b9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80719490"
---
# <a name="idebugstackframe3interceptcurrentexception"></a>IDebugStackFrame3::InterceptCurrentException
当当前堆栈帧上的调试器调用它想要截获当前异常时。

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

## <a name="parameters"></a>参数
`dwFlags`\
中指定不同的操作。 目前仅支持 [INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md) 值， `IEA_INTERCEPT` 并且必须指定。

`pqwCookie`\
弄标识特定异常的唯一值。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

 下面是最常见的错误返回。

|错误|说明|
|-----------|-----------------|
|`E_EXCEPTION_CANNOT_BE_INTERCEPTED`|无法截获当前异常。|
|`E_EXCEPTION_CANNOT_UNWIND_ABOVE_CALLBACK`|尚未在当前执行框架中搜索处理程序。|
|`E_INTERCEPT_CURRENT_EXCEPTION_NOT_SUPPORTED`|此帧不支持此方法。|

## <a name="remarks"></a>备注
 当引发异常时，调试器将在异常处理过程中从运行时获得控制。 在这段时间内，如果该帧要截获异常，则调试器可以询问当前堆栈帧。 通过这种方式，截获的异常实质上是堆栈帧的即时异常处理程序，即使该堆栈帧没有异常处理程序 (例如，程序代码) 中的 try/catch 块。

 当调试器需要知道是否应截获异常时，它会对当前堆栈帧对象调用此方法。 此方法负责处理异常的所有详细信息。 如果未实现 [IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md) 接口或 `InterceptStackException` 方法返回任何错误，则调试器会继续正常处理异常。

> [!NOTE]
> 异常只能在托管代码中截取，也就是说，当正在调试的程序在 .NET 运行时运行时。 当然，第三方语言实现者可以 `InterceptStackException` 在其自己的调试引擎中实现，如果选择了。

 截获完成后， [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md) 将收到信号。

## <a name="see-also"></a>另请参阅
- [IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)
- [INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md)
- [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)
