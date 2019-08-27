---
title: IDebugExceptionEvent2::GetException | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::GetException
helpviewer_keywords:
- IDebugExceptionEvent2::GetException
ms.assetid: 7c98f41d-322b-4e72-a514-cbd4823eb70d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 691df8f5a212f1d854d87076a215402c7ce0053c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310511"
---
# <a name="idebugexceptionevent2getexception"></a>IDebugExceptionEvent2::GetException
获取触发此事件的异常的详细的说明。

## <a name="syntax"></a>语法

```cpp
HRESULT GetException( 
   EXCEPTION_INFO* pExceptionInfo
);
```

```csharp
int GetException( 
   EXCEPTION_INFO[] pExceptionInfo
);
```

## <a name="parameters"></a>参数
`pExceptionInfo`\
[in、 out][EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)使用异常的说明填充的结构。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注

 [C++仅]调用方负责释放中的任何字符串[EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)结构，以及释放[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)结构中的对象。

## <a name="see-also"></a>请参阅
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)