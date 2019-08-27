---
title: IDebugStackFrame3::GetUnwindCodeContext | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame3::GetUnwindCodeContext
helpviewer_keywords:
- IDebugStackFrame3::GetUnwindCodeContext method
ms.assetid: b25f7e7d-2b24-48e4-93b3-829e61d73ebf
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a63883b8c2f1f7e09070173281f5e9eeda528352
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352089"
---
# <a name="idebugstackframe3getunwindcodecontext"></a>IDebugStackFrame3::GetUnwindCodeContext
返回代码上下文表示的位置，如果一个堆栈展开操作发生。

## <a name="syntax"></a>语法

```cpp
HRESULT GetUnwindCodeContext(
   IDebugCodeContext2 **ppCodeContext
);
```

```csharp
int GetUnwindCodeContext(
   out IDebugCodeContext2 ppCodeContext
);
```

## <a name="parameters"></a>参数
`ppCodeContext`\
[out]返回[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)对象，表示代码上下文位置，如果发生堆栈展开。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 尽管此方法可能会在堆栈展开之后返回位置的代码上下文，它并不意味着堆栈展开实际上可以发生在当前堆栈帧。

## <a name="see-also"></a>请参阅
- [IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)