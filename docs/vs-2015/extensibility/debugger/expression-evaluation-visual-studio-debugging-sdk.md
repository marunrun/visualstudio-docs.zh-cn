---
title: Visual Studio 调试 SDK) 的表达式计算 (|Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5044ced5-c18c-4534-b0bf-cc3e50cd57ac
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0f2a84f01168dd01921d933a80fe052c1a6c6447
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62562154"
---
# <a name="expression-evaluation-visual-studio-debugging-sdk"></a>表达式计算 (Visual Studio Debugging SDK)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在中断模式期间，IDE 必须能够评估涉及程序的多个变量的简单表达式。 若要实现此目的，调试引擎 (DE) 必须能够分析和计算输入到 IDE 的某个窗口中的表达式。  
  
 表达式是使用 [IDebugExpressionContext2：:P arsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 方法创建的，由生成的 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 接口表示。  
  
 **IDebugExpression2**接口由 DE 实现并调用其**EvalAsync**方法将[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)接口返回到 ide，以便在 ide 中显示表达式计算的结果。 [IDebugProperty2：： GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) 返回一个结构，该结构可用于将表达式的值放入监视窗口或放入 "局部变量" 窗口中。  
  
 调试包或会话调试管理器 (SDM) 调用 [IDebugExpression2：： EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 或 [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 获取表示求值结果的 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 接口。 `IDebugProperty2` 具有返回表达式的名称、类型和值的方法。 此信息显示在各种调试器窗口中。  
  
## <a name="using-expression-evaluation"></a>使用表达式计算  
 若要使用表达式计算，必须实现 [IDebugExpressionContext2：:P arsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 方法和 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 接口的所有方法，如下表所示。  
  
|方法|说明|  
|------------|-----------------|  
|[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|以异步方式计算表达式。|  
|[中断](../../extensibility/debugger/reference/idebugexpression2-abort.md)|结束异步表达式计算。|  
|[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|同步计算表达式。|  
  
 同步和异步评估要求实现 [IDebugProperty2：： GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) 方法。 异步表达式计算需要实现 [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)。  
  
## <a name="see-also"></a>另请参阅  
 [执行控件和状态计算](../../extensibility/debugger/execution-control-and-state-evaluation.md)
