---
title: IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
helpviewer_keywords:
- IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
ms.assetid: 07b20866-e598-4783-9ecc-6aa8625c8804
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 58967be9befc7061ea8005009b1628966a93de0f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349509"
---
# <a name="idebuginterceptexceptioncompleteevent2getinterceptcookie"></a>IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
当已截获异常处理完成时调用。

## <a name="syntax"></a>语法

```cpp
HRESULT GetInterceptCookie(
   UINT64* pqwCookie
);
```

```csharp
int GetInterceptCookie(
   out ulong pqwCookie
);
```

## <a name="parameters"></a>参数
`pqwCookie`\
[out]与已截获异常关联的唯一值。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则返回错误代码。

## <a name="remarks"></a>备注
 之后[InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)方法完成后已截获异常处理，将发送[IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)事件。 该处理程序可以使用`GetInterceptCookie`方法来检索与异常关联的唯一值 (相同的值传递给`InterceptCurrentException`方法)。

## <a name="see-also"></a>请参阅
- [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)
- [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)