---
title: Visual Studio 调试 SDK) 的表达式计算 (|Microsoft Docs
description: 在中断模式期间，IDE 将计算涉及程序变量的表达式。 了解调试引擎如何分析和计算表达式。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5044ced5-c18c-4534-b0bf-cc3e50cd57ac
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8c398d9eb79a6b5fcd1a6851596ab8913faf32fa
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2020
ms.locfileid: "96560884"
---
# <a name="expression-evaluation-visual-studio-debugging-sdk"></a>Visual Studio 调试 SDK (的表达式计算) 
在中断模式期间，IDE 必须评估涉及多个程序变量的简单表达式。 若要完成其评估，调试引擎 (DE) 必须分析和计算输入到 IDE 的其中一个窗口中的表达式。

 表达式是使用 [IDebugExpressionContext2：:P arsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 方法创建的，并由生成的 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 接口表示。

 **IDebugExpression2** 接口由 DE 实现并调用其 **EvalAsync** 方法将 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)接口返回到 ide，以便在 ide 中显示表达式计算的结果。 [IDebugProperty2：： GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) 返回一个结构，该结构用于将表达式的值置于 " **监视** " 窗口或 " **局部变量** " 窗口中。

 调试包或会话调试管理器 (SDM) 调用 [IDebugExpression2：： EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 或 [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 获取表示求值结果的 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 接口。 `IDebugProperty2` 具有返回表达式的名称、类型和值的方法。 此信息显示在各种调试器窗口中。

## <a name="using-expression-evaluation"></a>使用表达式计算
 若要使用表达式计算，必须实现 [IDebugExpressionContext2：:P arsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 方法和 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 接口的所有方法，如下表所示。

|方法|描述|
|------------|-----------------|
|[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|以异步方式计算表达式。|
|[中断](../../extensibility/debugger/reference/idebugexpression2-abort.md)|结束异步表达式计算。|
|[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|同步计算表达式。|

 同步和异步计算要求实现 [IDebugProperty2：： GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) 方法。 异步表达式计算需要实现 [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)。

## <a name="see-also"></a>另请参阅
- [执行控制和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)
