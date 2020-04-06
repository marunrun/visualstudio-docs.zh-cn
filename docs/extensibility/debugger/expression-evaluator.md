---
title: 表达式赋值器 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738685"
---
# <a name="expression-evaluator"></a>表达式计算器
表达式赋值器 （EE） 检查语言的语法，以在运行时解析和评估变量和表达式，从而允许用户在 IDE 处于中断模式时查看它们。

## <a name="use-expression-evaluators"></a>使用表达式赋值器
 使用[ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)方法创建表达式，如下所示：

1. 调试引擎 （DE） 实现[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口。

2. 调试包从[IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)接口获取`IDebugExpressionContext2`对象，然后调用它上`IDebugStackFrame2::ParseText`的方法以获取[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)对象。

3. 调试包调用[评估同步](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)方法或[评估Async](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)方法来获取表达式的值。 `IDebugExpression2::EvaluateAsync`从命令/立即窗口调用。 所有其他 UI 组件`IDebugExpression2::EvaluateSync`调用 。

4. 表达式计算的结果是[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)对象，它包含表达式计算结果的名称、类型和值。

   在表达式计算期间，EE 需要来自符号提供程序组件的信息。 符号提供程序提供用于标识和理解解析表达式的符号信息。

   异步表达式计算完成后，DE 将通过会话调试管理器 （SDM） 发送异步事件，通知 IDE 表达式计算已完成。 然后，从调用`IDebugExpression2::EvaluateSync`方法返回评估结果。

## <a name="implementation-notes"></a>实现说明
 调试[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]引擎希望使用通用语言运行时 （CLR） 接口与表达式赋值器进行对话。 因此，与[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试引擎配合的表达式赋值器必须支持 CLR（可在 debugref.doc 中找到所有 CLR 调试接口的完整列表，该列表是 中的一[!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)]部分）。

## <a name="see-also"></a>请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)
