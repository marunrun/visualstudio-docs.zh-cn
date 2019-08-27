---
title: 表达式计算 (Visual Studio 调试 SDK) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5044ced5-c18c-4534-b0bf-cc3e50cd57ac
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0e1e09f2302a6bb8401dd8c9f2d7c48810d5ecdc
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353815"
---
# <a name="expression-evaluation-visual-studio-debugging-sdk"></a>表达式计算 (Visual Studio Debugging SDK)
在中断模式下，IDE 的计算结果必须涉及多个程序变量的简单表达式。 若要完成其评估，调试引擎 (DE) 必须分析和计算表达式，用于输入到其中一个 IDE 的窗口。

 与创建表达式[IDebugExpressionContext2::ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)方法，并用来生成表示[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)接口。

 **IDebugExpression2**接口实现通过 DE 并调用其**EvalAsync**方法以返回[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)到 IDE 中，以便显示接口在 IDE 中的表达式评估结果。 [IDebugProperty2::GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)返回的结构，用于将表达式的值放**观看**窗口或 into**局部变量**窗口。

 调试包或会话调试管理器 (SDM) 调用[IDebugExpression2::EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)或[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)若要获取[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)表示接口计算的结果。 `IDebugProperty2` 已返回名称、 类型和表达式的值的方法。 此信息显示在不同的调试器窗口中。

## <a name="using-expression-evaluation"></a>使用表达式计算
 若要使用表达式计算，必须实现[IDebugExpressionContext2::ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)方法和所有的方法[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)接口，如以下表中所示。

|方法|描述|
|------------|-----------------|
|[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|以异步方式计算表达式。|
|[Abort](../../extensibility/debugger/reference/idebugexpression2-abort.md)|结束异步表达式求值。|
|[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|以同步方式计算表达式。|

 同步和异步评估需要实现[IDebugProperty2::GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)方法。 异步表达式计算需要实现[IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)。

## <a name="see-also"></a>请参阅
- [执行控件和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)