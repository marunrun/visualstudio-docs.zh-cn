---
title: IDebugExpression2：：评估同步 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2::EvaluateAsync
helpviewer_keywords:
- IDebugExpression2::EvaluateAsync
ms.assetid: 848fe6cb-0759-42f2-890b-d2b551c527d6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2cd1eba56f8e3c5a1a779acc3330790e9ba2bc96
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729751"
---
# <a name="idebugexpression2evaluateasync"></a>IDebugExpression2::EvaluateAsync
此方法异步计算表达式。

## <a name="syntax"></a>语法

```cpp
HRESULT EvaluateAsync (
    EVALFLAGS             dwFlags,
    IDebugEventCallback2* pExprCallback
);
```

```csharp
int EvaluateAsync(
    enum_EVALFLAGS       dwFlags,
    IDebugEventCallback2 pExprCallback
);
```

## <a name="parameters"></a>参数
`dwFlags`\
[在][EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)枚举中的标志的组合，用于控制表达式计算。

`pExprCallback`\
[在]此参数始终为空值。

## <a name="return-value"></a>返回值
如果成功，返回`S_OK`;否则返回错误代码。 典型的错误代码是：

|错误|描述|
|-----------|-----------------|
|E_EVALUATE_BUSY_WITH_EVALUATION|目前正在计算另一个表达式，并且不支持同时计算表达式。|

## <a name="remarks"></a>备注
此方法应在开始表达式计算后立即返回。 成功计算表达式后，必须将[IDebugExpressionExpression 评估完成事件2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)发送到[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)事件回调，通过[附加](../../../extensibility/debugger/reference/idebugprogram2-attach.md)或[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)提供。

## <a name="example"></a>示例
下面的示例演示如何实现[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)接口的简单`CExpression`对象实现此方法。

```cpp
HRESULT CExpression::EvaluateAsync(EVALFLAGS dwFlags,
                                   IDebugEventCallback2* pExprCallback)
{
    // Set the aborted state to FALSE
    // in case the user tries to redo the evaluation after aborting.
    m_bAborted = FALSE;
    // Post the WM_EVAL_EXPR message in the message queue of the current thread.
    // This starts the expression evaluation on a background thread.
    PostThreadMessage(GetCurrentThreadId(), WM_EVAL_EXPR, 0, (LPARAM) this);
    return S_OK;
}
```

## <a name="see-also"></a>请参阅
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
- [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)
- [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
