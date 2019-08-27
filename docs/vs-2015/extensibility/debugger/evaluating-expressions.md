---
title: 计算表达式 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expressions [Debugging SDK], evaluating
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5ccfcc80-dea5-48a1-8bae-6a26f8d3bc56
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: caff42c2e203151c6bab7d50b41744c2469ab3c2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68151621"
---
# <a name="evaluating-expressions"></a>计算表达式
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

从自动、 监视、 快速监视，或即时 windows 中向下传递的字符串创建表达式。 当计算表达式时，它生成一个包含名称和类型的变量或参数，并且其值的可打印字符串。 此字符串显示在相应的 IDE 窗口。  
  
## <a name="implementation"></a>实现  
 当程序在断点处停止时计算的表达式。 由表示该表达式本身[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)接口，它表示已准备好绑定和评估给定的表达式计算上下文中的已分析的表达式。 堆栈帧确定表达式计算上下文，调试引擎 (DE) 提供通过实现[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口。  
  
 给定的用户字符串和一个[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口，调试引擎 (DE) 可以获取[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)接口的用户将字符串传递到[IDebugExpressionContext2::ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)方法。 返回的 IDebugExpression2 接口包含准备好进行评估的已分析的表达式。  
  
 与`IDebugExpression2`接口，DE 可以获取通过同步或异步表达式计算，表达式的值使用[IDebugExpression2::EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)或[IDebugExpression2::EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)。 此值，以及名称和类型的变量或参数，用于显示发送到 IDE。 值、 名称和类型表示由[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)接口。  
  
 若要启用表达式求值，DE 必须实现[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)并[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口。 同步和异步评估需要实现[IDebugProperty2::GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)方法。  
  
## <a name="see-also"></a>请参阅  
 [堆栈帧](../../extensibility/debugger/stack-frames.md)   
 [表达式计算上下文](../../extensibility/debugger/expression-evaluation-context.md)   
 [调试任务](../../extensibility/debugger/debugging-tasks.md)
