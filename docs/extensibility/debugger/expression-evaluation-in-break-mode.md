---
title: 中断模式下的表达式计算 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode, expression evaluation
- debugging [Debugging SDK], expression evaluation
- expression evaluation, break mode
ms.assetid: 34fe5b58-15d5-4387-a266-72120f90a4b6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bc09fc43bd9f0edea4f6dc32e5f37c387c045796
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738722"
---
# <a name="expression-evaluation-in-break-mode"></a>中断模式下的表达式计算
以下部分介绍调试器处于中断模式且必须执行表达式计算时发生的过程。

## <a name="expression-evaluation-process"></a>表达式评估过程
 以下是计算表达式所涉及的基本步骤：

1. 会话调试管理器 （SDM） 调用[IDebugStackFrame2：：：获取表达式上下文](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)以获得表达式上下文接口[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)。

2. 然后，SDM 调用[IDebugExpressionContext2：:ParseText，](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)该字符串将被解析。

3. 如果 ParseText 未返回S_OK，则返回错误的原因。

     -否则

     如果 ParseText 确实返回S_OK，则 SDM 可以调用[IDebugExpression2：：：计算同步](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)或[IDebugExpression2：：评估Async](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)从解析的表达式中获取最终值。

    - 使用`IDebugExpression2::EvaluateSync`时，给定的回调接口将传达评估的持续过程。 最终值在[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)接口中返回。

    - 使用`IDebugExpression2::EvaluateAsync`时，给定的回调接口将传达评估的持续过程。 评估完成后，评估 Async 将通过回调发送[IDebugExpression 评估完成事件 2 接口](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)。 使用此事件接口，最终值将生成[GetResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
