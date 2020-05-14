---
title: 表达式评估（可视化工作室调试 SDK） |微软文档
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
ms.openlocfilehash: e41179fd530818f5ac59aa54420ede1b4eafa1ec
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738709"
---
# <a name="expression-evaluation-visual-studio-debugging-sdk"></a>表达式评估（可视化工作室调试 SDK）
在中断模式下，IDE 必须计算涉及多个程序变量的简单表达式。 为了完成其计算，调试引擎 （DE） 必须解析和评估输入到 IDE 窗口之一的表达式。

 表达式使用[IDebugExpressionContext2：:ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)方法创建，并由生成的[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)接口表示。

 **IDebugExpression2**接口由 DE 实现，并调用其**EvalAsync**方法将[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)接口返回到 IDE，以便在 IDE 中显示表达式计算的结果。 [IDebugProperty2：getPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)返回一个结构，用于将表达式的值放入 **"监视"** 窗口或 **"局部变量"** 窗口中。

 调试包或会话调试管理器 （SDM） 调用[IDebugExpression2：：评估Async](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)或[评估同步](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)，以获得表示评估结果的[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)接口。 `IDebugProperty2`具有返回表达式的名称、类型和值的方法。 此信息将显示在各种调试器窗口中。

## <a name="using-expression-evaluation"></a>使用表达式计算
 要使用表达式计算，必须实现[IDebugExpressionContext2：:ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)方法以及[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)接口的所有方法，如下表所示。

|方法|描述|
|------------|-----------------|
|[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|异步计算表达式。|
|[中止](../../extensibility/debugger/reference/idebugexpression2-abort.md)|结束异步表达式计算。|
|[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|同步计算表达式。|

 同步和异步评估需要实现[IDebugProperty2：：getPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)方法。 异步表达式计算要求实现[IDebug表达式计算完成事件2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)。

## <a name="see-also"></a>请参阅
- [执行控制和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)
