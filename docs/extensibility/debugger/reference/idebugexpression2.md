---
title: IDebugExpression2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2
helpviewer_keywords:
- IDebugExpression2 interface
ms.assetid: f5e4b124-1e30-47c8-a511-80084a02dba5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c2e23ad4f673e4e150ea677d993c5b36a4e386c2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80729692"
---
# <a name="idebugexpression2"></a>IDebugExpression2
此接口表示已分析的表达式可用于绑定和计算。

## <a name="syntax"></a>语法

```
IDebugExpression2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎 (DE) 实现此接口，以表示可以进行计算的已分析表达式。

## <a name="notes-for-callers"></a>调用方说明
 对 [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 的调用返回此接口。 [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) 返回 [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) 接口。 仅当正在调试的程序已暂停且堆栈帧可用时，才能访问这些接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugExpression2` 。

|方法|说明|
|------------|-----------------|
|[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|以异步方式计算此表达式。|
|[中断](../../../extensibility/debugger/reference/idebugexpression2-abort.md)|结束异步表达式计算。|
|[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|同步计算此表达式。|

## <a name="remarks"></a>备注
 当程序停止时，会话调试管理器 (SDM) 通过调用 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)从 DE 获取堆栈帧。 SDM 随后调用 [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) 以获取 [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) 接口。 接下来，调用 [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 以创建 `IDebugExpression2` 接口，该接口表示可进行计算的已分析表达式。

 SDM 调用 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 或 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 以实际计算表达式，并生成一个值。

 在的实现中 `IDebugExpressionContext2::ParseText` ，DE 使用 COM 的 `CoCreateInstance` 函数实例化表达式计算器并获取 [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md) 接口 (参见接口) 中的示例 `IDebugExpressionEvaluator` 。 然后，调用 [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) 以获取 [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md) 接口。 此接口在的实现中使用 `IDebugExpression2::EvaluateSync` ， `IDebugExpression2::EvaluateAsync` 用于执行计算。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetExpression](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)
