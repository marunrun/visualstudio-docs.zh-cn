---
title: 评估监视窗口表达式 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Watch window expressions
- Watch window, expressions
- expression evaluation, Watch window expressions
ms.assetid: b07e72c7-60d3-4b30-8e3f-6db83454c348
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9cef2f27eec095ee7b136153ecb764feba9effbb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738836"
---
# <a name="evaluate-a-watch-window-expression"></a>评估监视窗口表达式
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 当执行暂停时，Visual Studio 调用调试引擎 （DE） 以确定其监视列表中每个表达式的当前值。 DE 使用表达式赋值器 （EE） 计算每个表达式，Visual Studio 在 **"监视"** 窗口中显示其值。

 以下是如何计算观察列表表达式的概述：

1. Visual Studio 调用 DE 的[GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)来获取可用于计算表达式的表达式上下文。

2. 对于监视列表中的每个表达式，Visual Studio 调用[ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)将表达式文本转换为已解析的表达式。

3. `IDebugExpressionContext2::ParseText`调用[Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)执行分析文本的实际工作并生成[IDebugParsed 表达式](../../extensibility/debugger/reference/idebugparsedexpression.md)对象。

4. `IDebugExpressionContext2::ParseText`创建[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)对象并将`IDebugParsedExpression`对象放入其中。 然后，`DebugExpression2`此 I 对象将返回到视觉工作室。

5. 可视化工作室调用[评估同步](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)来评估解析的表达式。

6. `IDebugExpression2::EvaluateSync`将调用传递到[评估同步](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)以执行实际评估，并生成返回到 Visual Studio 的[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)对象。

7. Visual Studio 调用[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)以获取表达式的值，然后显示在监视列表中。

## <a name="parse-then-evaluate"></a>分析然后评估
 由于分析复杂表达式可能比计算它需要更长的时间，因此计算表达式的过程分为两个步骤：1） 解析表达式，2） 计算解析表达式。 这样，计算可以发生多次，但表达式只需要分析一次。 中间解析表达式从[IDebugParsedExpression 表达式](../../extensibility/debugger/reference/idebugparsedexpression.md)对象的 EE 返回，该对象依次封装并从 DE 作为[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)对象返回。 对象`IDebugExpression`会将所有计算延迟到`IDebugParsedExpression`对象。

> [!NOTE]
> 即使 Visual Studio 假定这一点，EE 也不必遵守此两步过程;调用[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)时，EE 可以在同一步骤中分析和评估（例如，MyCEE 示例的工作原理）。 如果语言可以形成复杂的表达式，则可能需要将解析步骤与计算步骤分开。 当显示许多监视表达式时，这可以提高 Visual Studio 调试器的性能。

## <a name="in-this-section"></a>在本节中
 [表达式计算的样本实现](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md)使用 MyCEE 示例逐步完成表达式评估过程。

 [评估监视表达式](../../extensibility/debugger/evaluating-a-watch-expression.md)解释成功解析表达式后发生的情况。

## <a name="related-sections"></a>相关章节
 [评估上下文](../../extensibility/debugger/evaluation-context.md)提供调试引擎 （DE） 调用表达式赋值器 （EE） 时传递的参数。

## <a name="see-also"></a>请参阅
 [编写 CLR 表达式赋值器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
