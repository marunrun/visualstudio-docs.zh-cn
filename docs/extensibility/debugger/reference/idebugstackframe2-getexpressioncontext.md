---
title: IDebugStackFrame2：：获取表达式上下文 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetExpressionContext
helpviewer_keywords:
- IDebugStackFrame2::GetExpressionContext
ms.assetid: a2604e6a-502d-473b-868f-b11ac64c7a35
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fb1a075d04ed53fdbe2181975a56eddfcbc3b683
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719751"
---
# <a name="idebugstackframe2getexpressioncontext"></a>IDebugStackFrame2::GetExpressionContext
获取在堆栈框架和线程的当前上下文中进行表达式计算的计算上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT GetExpressionContext ( 
   IDebugExpressionContext2** ppExprCxt
);
```

```csharp
int GetExpressionContext ( 
   out IDebugExpressionContext2 ppExprCxt
);
```

## <a name="parameters"></a>参数
`ppExprCxt`\
[出]返回表示表达式计算上下文的[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 通常，表达式计算上下文可以被视为执行表达式计算的范围。 调用[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)方法来解析表达式，然后调用生成的[评估同步](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)或评估[Async](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)方法来计算解析的表达式。

## <a name="see-also"></a>请参阅
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
