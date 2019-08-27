---
title: 表达式计算器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expressions [Debugging SDK]
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: f9381b2f-99aa-426c-aea0-d9c15f3c859b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c9f990225cbff539281122d21d4773f6611f694f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353773"
---
# <a name="expression-evaluator"></a>表达式计算器
表达式计算器 (EE) 检查一种语言来分析和在运行时计算变量和表达式的语法使他们能够在 IDE 处于中断模式下时由用户查看。

## <a name="use-expression-evaluators"></a>使用表达式计算器
 使用创建表达式[ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)方法，按如下所示：

1. 调试引擎 (DE) 实现[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口。

2. 调试包获取`IDebugExpressionContext2`对象从[IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)接口，然后调用`IDebugStackFrame2::ParseText`方法以获取[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)对象。

3. 调试包调用[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)方法或[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)方法以获取表达式的值。 `IDebugExpression2::EvaluateAsync` 从命令中的即时窗口调用。 所有其他 UI 组件调用`IDebugExpression2::EvaluateSync`。

4. 表达式计算的结果是[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)对象，其中包含名称、 类型和表达式计算结果的值。

   在表达式计算期间 EE 需要符号提供程序组件中的信息。 符号提供程序提供了用于确定和了解分析得出的表达式的符号信息。

   完成异步表达式计算后，异步事件发送由通过会话调试管理器 (SDM) DE 以通知 IDE 表达式计算已完成。 和计算的结果然后返回到调用`IDebugExpression2::EvaluateSync`方法。

## <a name="implementation-notes"></a>实现说明
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的调试引擎预期要与使用公共语言运行时 (CLR) 接口，表达式计算器进行对话。 因此，表达式计算器，适用于[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的调试引擎必须支持 CLR (调试接口的所有 CLR 的完整列表可在 debugref.doc，它是一部分的[!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)])。

## <a name="see-also"></a>请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)