---
title: 表达式计算器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expressions [Debugging SDK]
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: f9381b2f-99aa-426c-aea0-d9c15f3c859b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a477aaceb57e6ccd2eb5125fcf9d8af9be59472b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738685"
---
# <a name="expression-evaluator"></a>表达式计算器
表达式计算器 (EE) 检查语言的语法，以便在运行时分析和评估变量和表达式，从而在 IDE 处于中断模式时，用户可以查看这些语法和表达式。

## <a name="use-expression-evaluators"></a>使用表达式计算器
 表达式是使用 [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 方法创建的，如下所示：

1. 调试引擎 (DE) 实现 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) 接口。

2. 调试包 `IDebugExpressionContext2` 从 [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) 接口获取一个对象，然后对 `IDebugStackFrame2::ParseText` 其调用方法以获取 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 对象。

3. 调试包调用 [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 方法或 [EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 方法来获取表达式的值。 `IDebugExpression2::EvaluateAsync` 从 "命令/即时" 窗口中调用。 所有其他 UI 组件都调用 `IDebugExpression2::EvaluateSync` 。

4. 表达式计算的结果是一个 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 对象，该对象包含表达式计算结果的名称、类型和值。

   在表达式计算过程中，EE 需要来自符号提供程序组件的信息。 符号提供程序提供用于标识和理解分析的表达式的符号信息。

   当异步表达式计算完成时，将通过会话调试管理器 (SDM) 发送异步事件，以通知 IDE 表达式计算已完成。 而且，计算结果将从对方法的调用返回 `IDebugExpression2::EvaluateSync` 。

## <a name="implementation-notes"></a>实现说明
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试引擎需要使用公共语言运行时 (CLR) 接口与表达式计算器进行通信。 因此，与调试引擎一起使用的表达式计算器 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 必须支持 clr (可以在 debugref.doc （这是) 的一部分）中找到所有 clr 调试接口的完整列表 [!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)] 。

## <a name="see-also"></a>另请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)
