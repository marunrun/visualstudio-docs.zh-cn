---
title: 计算监视窗口表达式 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Watch window expressions
- Watch window, expressions
- expression evaluation, Watch window expressions
ms.assetid: b07e72c7-60d3-4b30-8e3f-6db83454c348
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f13573cfecbd81f36e3b77e9b23beeaa558c08dc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840683"
---
# <a name="evaluating-a-watch-window-expression"></a>计算监视窗口表达式
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 当执行暂停时，Visual Studio 将调用调试引擎 (DE) 来确定其监视列表中每个表达式的当前值。 DE 使用表达式计算器 (EE) 计算每个表达式，Visual Studio 在 " **监视** " 窗口中显示其值。  
  
 下面概述了如何计算监视列表表达式：  
  
1. Visual Studio 将调用 DE 的 [GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) ，以获取可用于计算表达式的表达式上下文。  
  
2. 对于监视列表中的每个表达式，Visual Studio 会调用 [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 将表达式文本转换为分析的表达式。  
  
3. `IDebugExpressionContext2::ParseText` 调用 [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) 来执行分析文本的实际工作，并生成 [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) 对象。  
  
4. `IDebugExpressionContext2::ParseText` 创建一个 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 对象，并将该 `IDebugParsedExpression` 对象放入其中。 然后，将此 I `DebugExpression2` 对象返回到 Visual Studio。  
  
5. Visual Studio 将调用 [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 来计算分析后的表达式。  
  
6. `IDebugExpression2::EvaluateSync` 传递对 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) 的调用，以执行实际计算，并生成返回到 Visual Studio 的 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 对象。  
  
7. Visual Studio 将调用 [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) 来获取随后显示在监视列表中的表达式的值。  
  
## <a name="parse-then-evaluate"></a>分析后评估  
 由于分析复杂表达式所需的时间可能比计算复杂，因此，计算表达式的过程分为两个步骤： 1) 分析表达式，2) 计算分析的表达式。 这样一来，计算可能会出现多次，但表达式只需分析一次。 将从 [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) 对象中的 EE 返回中间分析的表达式，并将其作为 [IDEBUGEXPRESSION2](../../extensibility/debugger/reference/idebugexpression2.md) 对象从 DE 中进行封装和返回。 `IDebugExpression`对象将所有计算都遵从于 `IDebugParsedExpression` 对象。  
  
> [!NOTE]
> 尽管 Visual Studio 假定这样做，但不需要将 EE 与此两步过程保持不一样：调用 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) 时，EE 可以在同一步骤中分析和评估 (这是 MyCEE 示例的工作方式，例如) 。 如果你的语言可以构成复杂的表达式，你可能需要将分析步骤与评估步骤分离。 当显示许多监视表达式时，这可能会提高 Visual Studio 调试器的性能。  
  
## <a name="in-this-section"></a>本节内容  
 [表达式计算的实现示例](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md)  
 使用 MyCEE 示例逐步完成表达式计算的过程。  
  
 [计算监视表达式](../../extensibility/debugger/evaluating-a-watch-expression.md)  
 说明成功的表达式分析后会发生的情况。  
  
## <a name="related-sections"></a>相关章节  
 [计算上下文](../../extensibility/debugger/evaluation-context.md)  
 提供当调试引擎 (DE) 调用表达式计算器 (EE) 时传递的参数。  
  
## <a name="see-also"></a>另请参阅  
 [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
