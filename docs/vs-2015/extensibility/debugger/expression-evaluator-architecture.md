---
title: 表达式计算器体系结构 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- architecture, expression evaluators
- expression evaluators, architecture
- debugging [Debugging SDK], expression evaluators
ms.assetid: aad7c4c6-1dc1-4d32-b975-f1fdf76bdeda
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e8e0aa8f5cc45e0f6e012ecb3f0a27a22725a259
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840549"
---
# <a name="expression-evaluator-architecture"></a>表达式计算器体系结构
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 将专有语言集成到 Visual Studio 调试包意味着实现所需的表达式计算器 (EE) 接口，并 (SP) 和联编程序接口调用公共语言运行时符号提供程序。 SP 和联编程序对象与当前执行地址一起是在其中计算表达式的上下文。 这些接口生成和使用的信息表示 EE 体系结构中的关键概念。  
  
## <a name="overview"></a>概述  
  
### <a name="parsing-the-expression"></a>分析表达式  
 在调试程序时，将计算表达式的原因有很多，但在断点处停止正在调试的程序时， (由用户或异常) 导致的断点。 此时，Visual Studio 会从调试引擎获取堆栈帧（由 [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) 接口表示）， (DE) 。 然后，Visual Studio 会调用 [GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) 来获取 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) 接口。 此接口表示可在其中计算表达式的上下文; [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 是评估过程的入口点。 直到此点为止，所有接口都是通过 DE 实现的。  
  
 `IDebugExpressionContext2::ParseText`调用时，将实例化与发生断点的源文件的语言相关联的 EE (此时，此时还会在此时) 中实例化 SH。 EE 由 [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md) 接口表示。 然后，取消调用 [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) ，以将文本格式) 的 (表达式转换为分析后的表达式，以便进行评估。 此分析的表达式由 [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) 接口表示。 请注意，通常会分析表达式，此时不会计算该表达式。  
  
 DE 会创建一个实现 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 接口的对象，将该 `IDebugParsedExpression` 对象放入对象中 `IDebugExpression2` ，并从返回 `IDebugExpression2` 对象 `IDebugExpressionContext2::ParseText` 。  
  
### <a name="evaluating-the-expression"></a>计算表达式  
 Visual Studio 将调用 [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 或 [EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 来计算分析后的表达式。 这两种方法都调用 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) (`IDebugExpression2::EvaluateSync` 立即调用方法，同时 `IDebugExpression2::EvaluateAsync` 通过后台线程调用方法) 计算分析的表达式并返回表示已分析表达式的值和类型的 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 接口。 `IDebugParsedExpression::EvaluateSync` 使用提供的 SH、address 和联编程序将已分析的表达式转换为实际值，并由 `IDebugProperty2` 接口表示。  
  
### <a name="for-example"></a>例如  
 在正在运行的程序中命中断点后，用户可以选择在 " **快速监视** " 对话框中查看变量。 此对话框显示变量的名称、值和类型。 用户通常可以更改值。  
  
 显示 " **快速监视** " 对话框时，要检查的变量的名称将作为文本发送到 [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)。 这会返回一个 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 对象，该对象表示已分析的表达式（在本例中为变量）。 然后，调用[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)以生成一个 `IDebugProperty2` 对象，该对象表示变量的值和类型以及其名称。 此时会显示此信息。  
  
 如果用户更改变量的值，则将使用新值调用 [SetValueAsString](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md) ，这会更改内存中变量的值，因此在程序恢复运行时将使用它。  
  
 有关显示变量值的此过程的更多详细信息，请参阅 [显示局部变量](../../extensibility/debugger/displaying-locals.md) 。 有关如何更改变量的值的更多详细信息，请参阅 [更改本地的值](../../extensibility/debugger/changing-the-value-of-a-local.md) 。  
  
## <a name="in-this-section"></a>本节内容  
 [计算上下文](../../extensibility/debugger/evaluation-context.md)  
 提供在 DE 调用 EE 时传递的参数。  
  
 [键表达式计算器接口](../../extensibility/debugger/key-expression-evaluator-interfaces.md)  
 介绍编写 EE 时所需的关键接口以及计算上下文。  
  
## <a name="see-also"></a>另请参阅  
 [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)   
 [显示局部变量](../../extensibility/debugger/displaying-locals.md)   
 [更改局部值](../../extensibility/debugger/changing-the-value-of-a-local.md)
