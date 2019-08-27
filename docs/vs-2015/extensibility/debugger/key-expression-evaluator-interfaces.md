---
title: 键表达式计算器接口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, interfaces
ms.assetid: 1cac9aa3-0867-4e12-a16e-1e90abbc0fb6
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b9c01c59e732b777967cf49a61f17305f666325f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63430175"
---
# <a name="key-expression-evaluator-interfaces"></a>键表达式计算器接口
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 在编写时以及评估上下文的表达式计算器 (EE)，您应熟悉以下接口。  
  
## <a name="interface-descriptions"></a>界面说明  
  
- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)  
  
     具有单个方法[GetAddress](../../extensibility/debugger/reference/idebugaddress-getaddress.md)，后者将获取一种数据结构，表示当前执行点。 此数据结构是调试引擎 (DE) 将传递给三个参数之一[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)方法计算的表达式。 通常由符号提供程序实现此接口。  
  
- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)  
  
     具有[绑定](../../extensibility/debugger/reference/idebugbinder-bind.md)方法，获取包含当前值的符号的内存区域。 给定两个包含表示的方法，通过[IDebugObject](../../extensibility/debugger/reference/idebugobject.md)对象，并且符号自身，由表示[IDebugField](../../extensibility/debugger/reference/idebugfield.md)对象，`IDebugBinder::Bind`返回符号的值。 `IDebugBinder` 通常由 DE 实现。  
  
- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)  
  
     表示简单数据类型。 对于更复杂的类型，如数组和方法，使用的派生[IDebugArrayField](../../extensibility/debugger/reference/idebugarrayfield.md)并[IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md)接口，分别。 [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md)是另一个重要的派生的接口，它表示包含其他符号，如方法或类的符号。 `IDebugField`接口 （和其衍生产品） 通常由符号提供程序。  
  
     `IDebugField`对象可以是用于查找的名称和类型的符号，并可在一起[IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)对象，可用于查找其值。  
  
- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)  
  
     表示实际的运行时间值的符号位。 [将绑定](../../extensibility/debugger/reference/idebugbinder-bind.md)采用[IDebugField](../../extensibility/debugger/reference/idebugfield.md)对象，它表示一个符号，并返回[IDebugObject](../../extensibility/debugger/reference/idebugobject.md)对象。 [GetValue](../../extensibility/debugger/reference/idebugobject-getvalue.md)方法返回的内存缓冲区中的符号的值。 DE 通常实现此接口来表示在内存中属性的值。  
  
- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)  
  
     此接口表示表达式计算器本身。 关键方法是[分析](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)，它将返回[IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)接口。  
  
- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)  
  
     此接口表示可供计算的已分析的表达式。 关键方法是[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)后者表示值和类型的表达式将返回一个 IDebugProperty2。  
  
- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)  
  
     此接口表示一个值，其类型，并且表达式计算的结果。  
  
## <a name="see-also"></a>请参阅  
 [计算上下文](../../extensibility/debugger/evaluation-context.md)
