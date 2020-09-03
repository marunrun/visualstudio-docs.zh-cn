---
title: 中断模式下的表达式计算 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- break mode, expression evaluation
- debugging [Debugging SDK], expression evaluation
- expression evaluation, break mode
ms.assetid: 34fe5b58-15d5-4387-a266-72120f90a4b6
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 362e50e20519c358564d13ba169f706fe384ca5c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152763"
---
# <a name="expression-evaluation-in-break-mode"></a>中断模式中的表达式计算
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

下面介绍调试器处于中断模式时，必须执行表达式计算的过程。  
  
## <a name="expression-evaluation-process"></a>表达式计算过程  
 下面是对表达式进行计算时所涉及的基本步骤：  
  
1. 会话调试管理器 (SDM) 调用 [IDebugStackFrame2：： GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) 以获取表达式上下文接口 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)。  
  
2. 然后，SDM 用要分析的字符串调用 [IDebugExpressionContext2：:P arsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 。  
  
3. 如果 ParseText 未返回 S_OK，则返回错误原因。  
  
     本来  
  
     如果 ParseText 返回 S_OK，则 SDM 可以调用 [IDebugExpression2：： EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 或 [IDebugExpression2：： EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 来从分析的表达式中获取最终值。  
  
    - 在使用的情况下 `IDebugExpression2::EvaluateSync` ，给定的回调接口用于与计算的正在进行的进程通信。 在 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 接口中返回最终值。  
  
    - 在使用的情况下 `IDebugExpression2::EvaluateAsync` ，给定的回调接口用于与计算的正在进行的进程通信。 完成评估后，EvaluateAsync 将通过回调发送 [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) 接口。 利用此事件接口，可以通过 [GetResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)获取最终值。  
  
## <a name="see-also"></a>另请参阅  
 [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
