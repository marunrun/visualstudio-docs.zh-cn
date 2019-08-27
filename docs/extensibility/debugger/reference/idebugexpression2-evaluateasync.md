---
title: IDebugExpression2::EvaluateAsync | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2::EvaluateAsync
helpviewer_keywords:
- IDebugExpression2::EvaluateAsync
ms.assetid: 848fe6cb-0759-42f2-890b-d2b551c527d6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dd5c0c6c056dc72f3db49a9d666d6f2ba6295791
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66326017"
---
# <a name="idebugexpression2evaluateasync"></a>IDebugExpression2::EvaluateAsync
此方法以异步方式计算的表达式。

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
[in]中的标志的组合[EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)控制表达式求值的枚举。

`pExprCallback`\
[in]此参数始终是一个 null 值。

## <a name="return-value"></a>返回值
如果成功，则返回`S_OK`; 否则返回错误代码。 典型的错误代码是：

|Error|描述|
|-----------|-----------------|
|E_EVALUATE_BUSY_WITH_EVALUATION|当前正在计算另一个表达式，并且不支持同时表达式计算。|

## <a name="remarks"></a>备注
此方法应返回立即启动后将其表达式计算。 当已成功计算表达式时， [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)必须发送到[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)事件回调提供通过[附加](../../../extensibility/debugger/reference/idebugprogram2-attach.md)或[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)。

## <a name="example"></a>示例
下面的示例演示如何实现此方法对于简单`CExpression`对象，它实现[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)接口。

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
