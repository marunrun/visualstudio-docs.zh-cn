---
title: 键表达式计算器接口 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, interfaces
ms.assetid: 1cac9aa3-0867-4e12-a16e-1e90abbc0fb6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 01527edac4000f0b2f7b89fdd507fc093f0d7734
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738489"
---
# <a name="key-expression-evaluator-interfaces"></a>键表达式计算器接口
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 在编写表达式计算器 (EE) 以及计算上下文时，应熟悉以下接口。

## <a name="interface-descriptions"></a>接口说明

- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)

     具有一个 [GetAddress](../../extensibility/debugger/reference/idebugaddress-getaddress.md)，该方法可获取表示当前执行点的数据结构。 此数据结构是调试引擎 (DE) 传递给 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) 方法以计算表达式的三个参数之一。 此接口通常由符号提供程序实现。

- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)

     具有 [Bind](../../extensibility/debugger/reference/idebugbinder-bind.md) 方法，该方法可获取包含符号当前值的内存区域。 给定包含方法（由 [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) 对象表示）和符号本身（由 [IDebugField](../../extensibility/debugger/reference/idebugfield.md) 对象表示） `IDebugBinder::Bind` 返回符号的值。 `IDebugBinder` 通常由 DE 实现。

- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)

     表示简单的数据类型。 对于更复杂的类型（如数组和方法），请分别使用派生的 [IDebugArrayField](../../extensibility/debugger/reference/idebugarrayfield.md) 和 [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) 接口。 [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) 是另一个重要的派生接口，它表示包含其他符号的符号，如方法或类。 `IDebugField`接口 (及其派生) 通常由符号提供程序实现。

     `IDebugField`对象可用于查找符号的名称和类型，以及[IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)对象，可用于查找其值。

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

     表示符号的运行时值的实际位。 [Bind](../../extensibility/debugger/reference/idebugbinder-bind.md) 使用 [IDebugField](../../extensibility/debugger/reference/idebugfield.md) 对象，该对象表示一个符号，并返回 [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) 对象。 [GetValue](../../extensibility/debugger/reference/idebugobject-getvalue.md)方法返回内存缓冲区中的符号值。 DE 通常实现此接口，以在内存中表示属性的值。

- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)

     此接口表示表达式计算器本身。 关键方法为 [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)，这将返回 [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) 接口。

- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)

     此接口表示可以进行计算的已分析表达式。 Key 方法是 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) ，它返回表示表达式的值和类型的 IDebugProperty2。

- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)

     此接口表示一个值及其类型，并且是表达式计算的结果。

## <a name="see-also"></a>另请参阅
- [计算上下文](../../extensibility/debugger/evaluation-context.md)
