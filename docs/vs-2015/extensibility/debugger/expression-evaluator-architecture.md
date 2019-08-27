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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63421229"
---
# <a name="expression-evaluator-architecture"></a>表达式计算器体系结构
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 将专有语言集成到 Visual Studio 调试包意味着实现所需的表达式计算器 (EE) 接口和调用的公共语言运行时符号提供程序 (SP) 和绑定器接口。 SP 和联编程序对象，当前执行地址，以及是在其中计算表达式的上下文。 这些接口生成和使用的信息表示 EE 的体系结构中的关键概念。  
  
## <a name="overview"></a>概述  
  
### <a name="parsing-the-expression"></a>分析表达式  
 调试程序时，表达式的计算多个原因，但始终当正在调试的程序已停止在断点处 （由用户放置一个断点或一个引起的异常）。 由表示是在 Visual Studio 时获取堆栈帧，此时刻[IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)接口，从调试引擎 (DE)。 Visual Studio 然后调用[GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)来获取[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口。 此接口表示在其中可以计算表达式; 上下文[ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)是评估过程的入口点。 到目前为止，为止的所有接口由 DE 都实现。  
  
 当`IDebugExpressionContext2::ParseText`是调用，DE 实例化与断点发生的位置的源代码文件的语言关联 EE （DE 还实例化 SH 此时）。 由表示 EE [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)接口。 然后调用 DE[分析](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)要转换为已分析表达式 （以文本形式） 的表达式，可供评估。 此分析的表达式为由[IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)接口。 请注意，表达式是通常分析并不会在此时评估。  
  
 DE 创建实现的对象[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)接口，put`IDebugParsedExpression`对象插入`IDebugExpression2`对象，并返回`IDebugExpression2`对象从`IDebugExpressionContext2::ParseText`。  
  
### <a name="evaluating-the-expression"></a>对表达式求值  
 Visual Studio 会调用任一[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)或[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)已分析的表达式进行求值。 这两种方法调用[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) (`IDebugExpression2::EvaluateSync`调用的方法立即，尽管`IDebugExpression2::EvaluateAsync`调用通过后台线程方法) 来计算已分析的表达式并返回[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)表示的值和分析的表达式的类型的接口。 `IDebugParsedExpression::EvaluateSync` 使用提供的 SH、 地址和绑定器来分析得出的表达式转换为实际值，表示`IDebugProperty2`接口。  
  
### <a name="for-example"></a>例如  
 在正在运行的程序命中断点后，用户选择查看中的变量**快速监视**对话框。 此对话框显示变量的名称、 其值和它的类型。 通常，用户可以更改值。  
  
 当**快速监视**对话框中所示，要检查变量的名称发送以文本形式向[ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)。 这将返回[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)对象，表示已分析的表达式，在这种情况下，该变量。 [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)然后调用以生成`IDebugProperty2`对象，表示变量的值和类型，以及它的名称。 它是显示此信息。  
  
 如果用户更改变量的值[SetValueAsString](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)调用使用新值，更改在内存中变量的值，以使程序恢复运行时将使用它运行。  
  
 请参阅[显示局部变量](../../extensibility/debugger/displaying-locals.md)有关显示变量的值的此过程的详细信息。 请参阅[更改局部值](../../extensibility/debugger/changing-the-value-of-a-local.md)有关如何更改变量的值的详细信息。  
  
## <a name="in-this-section"></a>本节内容  
 [计算上下文](../../extensibility/debugger/evaluation-context.md)  
 提供当 DE 调用 EE 时传递的参数。  
  
 [键表达式计算器接口](../../extensibility/debugger/key-expression-evaluator-interfaces.md)  
 描述需要编写 EE，以及评估上下文时的重要接口。  
  
## <a name="see-also"></a>请参阅  
 [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)   
 [显示局部](../../extensibility/debugger/displaying-locals.md)   
 [更改局部值](../../extensibility/debugger/changing-the-value-of-a-local.md)
