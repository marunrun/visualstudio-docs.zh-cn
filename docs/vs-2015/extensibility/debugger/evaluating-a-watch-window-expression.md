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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444798"
---
# <a name="evaluating-a-watch-window-expression"></a>计算监视窗口表达式
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 当将暂停执行时，Visual Studio 调用调试引擎 (DE) 来确定其监视列表中的每个表达式的当前值。 DE 每个使用计算表达式的表达式计算器 (EE) 和 Visual Studio 将显示在其值**监视**窗口。  
  
 下面是概述如何评估监视列表表达式：  
  
1. Visual Studio 会调用 DE [GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)若要获取可用于计算表达式的表达式上下文。  
  
2. 监视列表中每个表达式，Visual Studio 会调用[ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)将表达式文本转换为已分析的表达式。  
  
3. `IDebugExpressionContext2::ParseText` 调用[分析](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)若要执行的分析的文本和生成的实际工作[IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)对象。  
  
4. `IDebugExpressionContext2::ParseText` 创建[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)对象，并会使`IDebugParsedExpression`到其中的对象。 此我`DebugExpression2`对象然后返回到 Visual Studio。  
  
5. Visual Studio 调用[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)已分析的表达式进行求值。  
  
6. `IDebugExpression2::EvaluateSync` 将传递到调用[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)若要执行的实际计算并生成[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)返回到 Visual Studio 的对象。  
  
7. Visual Studio 调用[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)以获取然后监视列表中显示的表达式的值。  
  
## <a name="parse-then-evaluate"></a>分析并评估  
 分析复杂表达式可能需要更长时间对其进行评估，因为表达式的计算过程分成了两个步骤：1) 分析表达式和 2） 的计算结果的已分析的表达式。 这样一来，评估可能会发生很多时候但需要进行一次分析该表达式。 中间分析得出的表达式返回从 EE [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)对象，进而封装并返回从作为 DE [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)对象。 `IDebugExpression`对象将所有计算交都由`IDebugParsedExpression`对象。  
  
> [!NOTE]
> 不遵守此两步过程，即使 Visual Studio 假设这一点; EE 的必要条件EE 可以分析和评估在相同的步骤时[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)称为 （这是 MyCEE 示例的工作方式，例如）。 如果你的语言可以构成复杂的表达式，您可能想要单独评估步骤中的分析。 许多监视表达式时，这可以提高在 Visual Studio 调试器中的性能显示。  
  
## <a name="in-this-section"></a>本节内容  
 [表达式计算的实现示例](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md)  
 使用 MyCEE 样本来单步执行的表达式计算过程。  
  
 [计算监视表达式](../../extensibility/debugger/evaluating-a-watch-expression.md)  
 介绍了成功的表达式分析后发生的情况。  
  
## <a name="related-sections"></a>相关章节  
 [计算上下文](../../extensibility/debugger/evaluation-context.md)  
 提供调试引擎 (DE) 调用表达式计算器 (EE) 时传递的参数。  
  
## <a name="see-also"></a>请参阅  
 [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
