---
title: IDebugEngine2::SetException |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::SetException
helpviewer_keywords:
- IDebugEngine2::SetException
ms.assetid: e6f5ec48-09e8-4b9b-9dc9-55f8d883f1b7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2234c0c0b571e763d3b143b5606fe61c43f25cde
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352530"
---
# <a name="idebugengine2setexception"></a>IDebugEngine2::SetException
指定调试引擎 (DE) 应如何处理给定的异常。

## <a name="syntax"></a>语法

```cpp
HRESULT SetException( 
   EXCEPTION_INFO* pException
);
```

```csharp
int SetException( 
   EXCEPTION_INFO[] pException
);
```

## <a name="parameters"></a>参数
`pException`\
[in][EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)介绍异常以及如何对其进行调试的结构。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 可以指示 DE 停止生成第一次机会在异常的程序，第二次机会，或根本不容易。

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)