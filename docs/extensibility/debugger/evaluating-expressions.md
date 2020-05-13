---
title: 计算表达式 |微软文档
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
ms.openlocfilehash: 18e342704cbb4abd7de9667576ce331ef8fbf60a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738829"
---
# <a name="evaluate-expressions"></a>计算表达式
表达式是从从**自动**、**监视**、**快速监视**或**即时**窗口向下传递的字符串创建的。 计算表达式时，它生成一个可打印字符串，其中包含变量或参数的名称和类型及其值。 此字符串显示在相应的 IDE 窗口中。

## <a name="implementation"></a>实现
 当程序在断点停止时，将计算表达式。 表达式本身由[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)接口表示，该接口表示已解析的表达式，该表达式可用于在给定的表达式计算上下文中进行绑定和评估。 堆栈帧确定表达式计算上下文，调试引擎 （DE） 通过实现[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口来提供该上下文。

 给定用户字符串和[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口，调试引擎 （DE） 可以通过将用户字符串传递给[IDebugExpressionContext2：:ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)方法来获取[IDebugExpressionExpression2](../../extensibility/debugger/reference/idebugexpression2.md)接口。 返回的 IDebugExpression2 接口包含可供评估的解析表达式。

 通过`IDebugExpression2`该接口，DE可以通过同步或异步表达式计算获得表达式的值，使用[IDebugExpression2：：：计算同步](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)或[IDebugExpression2：：评估Async](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)。 此值以及变量或参数的名称和类型将发送到 IDE 进行显示。 值、名称和类型由[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)接口表示。

 要启用表达式计算，DE 必须实现[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)和[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口。 同步和异步计算都需要[IDebugProperty2：：：getPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)方法的实现。

## <a name="see-also"></a>请参阅
- [堆叠帧](../../extensibility/debugger/stack-frames.md)
- [表达式计算上下文](../../extensibility/debugger/expression-evaluation-context.md)
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
