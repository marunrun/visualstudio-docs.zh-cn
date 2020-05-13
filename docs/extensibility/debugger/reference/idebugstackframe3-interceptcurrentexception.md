---
title: IDebugStackFrame3：：拦截电流异常 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719490"
---
# <a name="idebugstackframe3interceptcurrentexception"></a>IDebugStackFrame3::InterceptCurrentException
当前堆栈帧上的调试器在要拦截当前异常时调用它。

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
[在]指定不同的操作。 目前，仅支持[INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md)值`IEA_INTERCEPT`，并且必须指定。

`pqwCookie`\
[出]标识特定异常的唯一值。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

 以下是最常见的错误返回。

|错误|描述|
|-----------|-----------------|
|`E_EXCEPTION_CANNOT_BE_INTERCEPTED`|无法截获当前异常。|
|`E_EXCEPTION_CANNOT_UNWIND_ABOVE_CALLBACK`|当前执行帧尚未搜索处理程序。|
|`E_INTERCEPT_CURRENT_EXCEPTION_NOT_SUPPORTED`|此帧不支持此方法。|

## <a name="remarks"></a>备注
 引发异常时，调试器在异常处理过程中从关键点的运行时获得控制。 在这些关键时刻，调试器可以询问当前堆栈帧，如果帧想要拦截异常。 这样，被截获的异常实质上是堆栈帧的即时异常处理程序，即使该堆栈帧没有异常处理程序（例如，程序代码中的 try/catch 块）。

 当调试器想知道是否应截获异常时，它会在当前堆栈帧对象上调用此方法。 此方法负责处理异常的所有详细信息。 如果未实现[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)接口，或者`InterceptStackException`该方法返回任何错误，则调试器将继续正常处理异常。

> [!NOTE]
> 异常只能在托管代码中截获，也就是说，当正在调试的程序在 .NET 运行时运行时。 当然，如果第三方语言实现者愿意，`InterceptStackException`可以在自己的调试引擎中实现。

 拦截完成后，发出[IDebug拦截异常完成事件 2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)的信号。

## <a name="see-also"></a>请参阅
- [IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)
- [INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md)
- [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)
