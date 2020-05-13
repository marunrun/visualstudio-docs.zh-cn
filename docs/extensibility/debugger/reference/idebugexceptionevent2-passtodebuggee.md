---
title: IDebugexception2：:PasstoDebuggee |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::PassToDebuggee
helpviewer_keywords:
- IDebugExceptionEvent2::PassToDebuggee
ms.assetid: a20d0f0b-2ca0-4437-bd22-9213c81d2738
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: aec6f460295b59b2b5455b83d5b0be554bca24fa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729832"
---
# <a name="idebugexceptionevent2passtodebuggee"></a>IDebugExceptionEvent2::PassToDebuggee
指定是否应将异常传递到执行恢复时正在调试的程序，还是应丢弃该异常。

## <a name="syntax"></a>语法

```cpp
HRESULT PassToDebuggee(
   BOOL fPass
);
```

```csharp
int PassToDebuggee(
   int fPass
);
```

## <a name="parameters"></a>参数
`fPass`\
[在]如果异常应在`TRUE`执行恢复时传递给正在调试的程序，则为非零 （ ）， 如果应丢弃异常，`FALSE`则为零 （）。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法实际上不会导致在正在调试的程序中执行任何代码。 调用只是为了为下一个代码执行设置状态。 例如，对[CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)方法的调用可能会`S_OK`随[EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)返回。`dwState` 字段设置为`EXCEPTION_STOP_SECOND_CHANCE`。

 IDE 可能会接收[IDebugExceptionEvent2 事件](../../../extensibility/debugger/reference/idebugexceptionevent2.md)并调用["继续"](../../../extensibility/debugger/reference/idebugprogram2-continue.md)方法。 如果不调用方法，调试引擎 （DE） 应具有处理该情况的`PassToDebuggee`默认行为。

## <a name="see-also"></a>请参阅
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)
- [继续](../../../extensibility/debugger/reference/idebugprogram2-continue.md)
