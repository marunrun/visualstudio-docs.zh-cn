---
title: 表达式赋值器实现策略 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, implementation strategy
- debug engines, implementation strategies
ms.assetid: 1bccaeb3-8109-4128-ae79-16fd8fbbaaa2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3922689c20c839b3c0c2b2440bc9fefd5d25c80a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738672"
---
# <a name="expression-evaluator-implementation-strategy"></a>表达式赋值器实现策略
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 快速创建表达式赋值器 （EE） 的一种方法是首先实现在 **"局部变量"** 窗口中显示局部变量所需的最小代码。 必须认识到"**局部变量"** 窗口中的每一行都显示局部变量的名称、类型和值，并且所有三行都由[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)对象表示。 局部变量的名称、类型和值通过调用其[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) `IDebugProperty2`方法从对象获得。 有关如何在 **"局部变量"** 窗口中显示局部变量的详细信息，请参阅[显示局部变量](../../extensibility/debugger/displaying-locals.md)。

## <a name="discussion"></a>讨论区
 可能的实现序列从实现[IDebugExpression 赋值器](../../extensibility/debugger/reference/idebugexpressionevaluator.md)开始。 必须实现[分析](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)法和[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)方法以显示局部变量。 调用`IDebugExpressionEvaluator::GetMethodProperty`返回表示`IDebugProperty2`方法的对象：即[IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md)对象。 方法本身不显示在 **"局部变量"** 窗口中。

 接下来应实现[枚举子](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)方法。 调试引擎 （DE） 调用此方法，通过传递`IDebugProperty2::EnumChildren`的`guidFilter``guidFilterLocalsPlusArgs`参数来获取本地变量和参数的列表。 `IDebugProperty2::EnumChildren`调用[枚举](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)和[枚举，](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)将结果合并到单个枚举中。 有关详细信息[，请参阅显示局部变量](../../extensibility/debugger/displaying-locals.md)。

## <a name="see-also"></a>请参阅
- [实现表达式赋值器](../../extensibility/debugger/implementing-an-expression-evaluator.md)
- [显示局部变量](../../extensibility/debugger/displaying-locals.md)
