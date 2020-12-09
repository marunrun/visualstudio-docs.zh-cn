---
title: 计算表达式 |Microsoft Docs
description: 了解如何计算表达式，这些表达式是从 "自动"、"监视"、"快速监视" 或 "即时" 窗口中传递的字符串创建的。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expressions [Debugging SDK], evaluating
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5ccfcc80-dea5-48a1-8bae-6a26f8d3bc56
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b43fc91de129407f2fd01e12951cffee4028186f
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "96914590"
---
# <a name="evaluate-expressions"></a>计算表达式
表达式是通过 **从 "自动**"、" **监视**"、" **快速监视**" 或 " **即时** " 窗口中传递的字符串创建的。 计算表达式时，它将生成一个可打印字符串，其中包含变量或参数的名称和类型及其值。 此字符串将显示在相应的 IDE 窗口中。

## <a name="implementation"></a>实现
 当程序在断点处停止时，将计算表达式。 表达式本身由 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 接口表示，后者表示已分析的表达式，该表达式可用于给定表达式计算上下文中的绑定和计算。 堆栈帧确定表达式计算上下文，调试引擎 (通过实现 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) 接口) 提供。

 给定用户字符串和[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口，调试引擎 (DE) 可以通过将用户字符串传递到[IDebugExpressionContext2：:P arsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)方法来获取[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)接口。 返回的 IDebugExpression2 接口包含可用于计算的已分析表达式。

 使用 `IDebugExpression2` 接口时，可以使用 [IDebugExpression2：： EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 或 [IDebugExpression2：： EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)通过同步或异步表达式计算来获取表达式的值。 此值与变量或参数的名称和类型一起发送到 IDE 以显示。 值、名称和类型由 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 接口表示。

 若要启用表达式求值，DE 必须实现 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 和 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) 接口。 同步和异步计算都需要实现 [IDebugProperty2：： GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) 方法。

## <a name="see-also"></a>另请参阅
- [堆栈帧](../../extensibility/debugger/stack-frames.md)
- [表达式计算上下文](../../extensibility/debugger/expression-evaluation-context.md)
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
