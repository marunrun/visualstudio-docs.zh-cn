---
title: 表达式评估器体系结构 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- architecture, expression evaluators
- expression evaluators, architecture
- debugging [Debugging SDK], expression evaluators
ms.assetid: aad7c4c6-1dc1-4d32-b975-f1fdf76bdeda
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aac782c653f230d5598a49d43eb70f548de6dc41
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738695"
---
# <a name="expression-evaluator-architecture"></a>表达式赋值器体系结构
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 将专有语言集成到 Visual Studio 调试包中意味着必须设置所需的表达式赋值器 （EE） 接口，并调用通用语言运行时符号提供程序 （SP） 和粘合剂接口。 SP 和活页夹对象以及当前执行地址是计算表达式的上下文。 这些接口产生和使用的信息代表了 EE 体系结构中的关键概念。

## <a name="overview"></a>概述

### <a name="parse-the-expression"></a>解析表达式
 调试程序时，表达式的计算原因有很多，但总是在正在调试的程序在断点停止时（用户放置的断点或由异常引起的断点）。 此时，Visual Studio 从调试引擎 （DE） 获取一个堆栈帧，由[IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)接口表示。 然后，可视化工作室调用[GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)来获取[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)界面。 此接口表示可以计算表达式的上下文;[分析文本](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)是评估过程的入口点。 在此之前，所有接口都由 DE 实现。

 调用`IDebugExpressionContext2::ParseText`时，DE 实例化与发生断点的源文件的语言关联的 EE（此时 DE 还会实例化 SH）。 EE 由[IDebugExpression 评估器](../../extensibility/debugger/reference/idebugexpressionevaluator.md)接口表示。 然后，DE 调用[Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)将表达式（文本形式）转换为已解析的表达式，以便进行计算。 此解析表达式由[IDebugParsed 表达式](../../extensibility/debugger/reference/idebugparsedexpression.md)接口表示。 表达式通常被解析，此时不计算。

 DE 创建一个实现[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)接口的对象，将`IDebugParsedExpression`对象放入对象`IDebugExpression2`，并从 中返回`IDebugExpression2`该对象`IDebugExpressionContext2::ParseText`。

### <a name="evaluate-the-expression"></a>计算表达式
 Visual Studio 调用[评估同步](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)或[评估 Async](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)以评估解析的表达式。 这两种方法都调用[EvaluateSync（](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)`IDebugExpression2::EvaluateSync`立即调用方法，同时`IDebugExpression2::EvaluateAsync`通过后台线程调用方法），以评估解析的表达式并返回表示解析表达式的值和类型的[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)接口。 `IDebugParsedExpression::EvaluateSync`使用提供的 SH、地址和活页夹将解析的表达式转换为实际值，该值由`IDebugProperty2`接口表示。

### <a name="for-example"></a>例如：
 在正在运行的程序中命中断点后，用户选择在**QuickWatch**对话框中查看变量。 此对话框显示变量的名称、值及其类型。 用户通常可以更改该值。

 显示 **"快速观察"** 对话框时，被检查的变量的名称将作为文本发送到[ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)。 这将返回表示解析表达式（本例中为变量）的[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)对象。 然后调用[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)以生成`IDebugProperty2`表示变量的值和类型以及其名称的对象。 显示的是此信息。

 如果用户更改变量的值，则使用新值调用[SetValueAsString，](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)该值会更改内存中变量的值，以便在程序继续运行时使用它。

 有关显示变量值的此过程的更多详细信息，请参阅[显示局部变量](../../extensibility/debugger/displaying-locals.md)。 有关如何更改变量值的更多详细信息[，请参阅更改本地值](../../extensibility/debugger/changing-the-value-of-a-local.md)。

## <a name="in-this-section"></a>在本节中
 [评估上下文](../../extensibility/debugger/evaluation-context.md)提供 DE 调用 EE 时传递的参数。

 [键表达式赋值器接口](../../extensibility/debugger/key-expression-evaluator-interfaces.md)描述编写 EE 时所需的关键接口以及评估上下文。

## <a name="see-also"></a>请参阅
- [编写 CLR 表达式赋值器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [显示本地变量](../../extensibility/debugger/displaying-locals.md)
- [更改本地值](../../extensibility/debugger/changing-the-value-of-a-local.md)
