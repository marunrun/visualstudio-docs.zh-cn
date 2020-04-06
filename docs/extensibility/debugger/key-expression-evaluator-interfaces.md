---
title: 键表达式赋值器接口 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738489"
---
# <a name="key-expression-evaluator-interfaces"></a>键表达式赋值器接口
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 编写表达式赋值器 （EE） 以及计算上下文时，应熟悉以下接口。

## <a name="interface-descriptions"></a>接口描述

- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)

     具有单个方法[GetAddress](../../extensibility/debugger/reference/idebugaddress-getaddress.md)，它获取表示当前执行点的数据结构。 此数据结构是调试引擎 （DE） 传递给[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)方法以评估表达式的三个参数之一。 此接口通常由符号提供程序实现。

- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)

     具有[Bind](../../extensibility/debugger/reference/idebugbinder-bind.md)方法，该方法获取包含符号当前值的内存区域。 给定包含方法（由[IDebugObject 对象](../../extensibility/debugger/reference/idebugobject.md)表示）和符号本身（由[IDebugField](../../extensibility/debugger/reference/idebugfield.md)对象表示）`IDebugBinder::Bind`都会返回符号的值。 `IDebugBinder`通常由 DE 实现。

- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)

     表示简单的数据类型。 对于更复杂的类型（如数组和方法），分别使用派生的[IDebugArrayField](../../extensibility/debugger/reference/idebugarrayfield.md)和[IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md)接口。 [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md)是另一个重要的派生接口，它表示包含其他符号（如方法或类）的符号。 接口`IDebugField`（及其衍生物）通常由符号提供程序实现。

     对象`IDebugField`可用于查找符号的名称和类型，并且与[IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)对象一起可用于查找其值。

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

     表示符号的运行时值的实际位。 [绑定](../../extensibility/debugger/reference/idebugbinder-bind.md)采用[IDebugField](../../extensibility/debugger/reference/idebugfield.md)对象，该对象表示符号，并返回[IDebugObject 对象](../../extensibility/debugger/reference/idebugobject.md)。 [GetValue](../../extensibility/debugger/reference/idebugobject-getvalue.md)方法返回内存缓冲区中符号的值。 DE 通常实现此接口以表示内存中属性的值。

- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)

     此接口表示表达式赋值器本身。 键方法是[Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)，它返回[IDebugparsed 表达式](../../extensibility/debugger/reference/idebugparsedexpression.md)接口。

- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)

     此接口表示可供计算的已解析表达式。 键方法是[评估同步](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)，它返回表示表达式的值和类型的 IDebugProperty2。

- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)

     此接口表示值及其类型，是表达式计算的结果。

## <a name="see-also"></a>请参阅
- [评估上下文](../../extensibility/debugger/evaluation-context.md)
