---
title: IDebugExpression2 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729692"
---
# <a name="idebugexpression2"></a>IDebugExpression2
此接口表示可供绑定和评估的解析表达式。

## <a name="syntax"></a>语法

```
IDebugExpression2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口以表示准备计算的解析表达式。

## <a name="notes-for-callers"></a>呼叫者备注
 对[ParseText 的](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)调用将返回此接口。 [getExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)返回[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口。 仅当正在调试的程序已暂停且堆栈帧可用时，才能访问这些接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugExpression2`。

|方法|描述|
|------------|-----------------|
|[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|异步计算此表达式。|
|[中止](../../../extensibility/debugger/reference/idebugexpression2-abort.md)|结束异步表达式计算。|
|[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|同步计算此表达式。|

## <a name="remarks"></a>备注
 当程序停止时，会话调试管理器 （SDM） 从 DE 获取一个堆栈帧，并调用[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)。 然后，SDM 调用[GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)来获取[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口。 然后调用[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)以创建`IDebugExpression2`接口，该接口表示可计算的解析表达式。

 SDM 调用[评估同步](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)或[评估 Async](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)来实际评估表达式并生成值。

 在实现 中`IDebugExpressionContext2::ParseText`，DE 使用 COM 的`CoCreateInstance`函数实例化表达式赋值器并获得[IDebugExpression 评估器](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)接口（请参阅界面中`IDebugExpressionEvaluator`的示例）。 然后，DE 调用[Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)以获取[IDebugparsed 表达式](../../../extensibility/debugger/reference/idebugparsedexpression.md)接口。 此接口用于实现`IDebugExpression2::EvaluateSync`和执行`IDebugExpression2::EvaluateAsync`评估。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetExpression](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)
