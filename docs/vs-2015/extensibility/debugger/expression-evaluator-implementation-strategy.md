---
title: 表达式计算器实施策略 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, implementation strategy
- debug engines, implementation strategies
ms.assetid: 1bccaeb3-8109-4128-ae79-16fd8fbbaaa2
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a9c2ded111c371fc1a42c8f1ee08769f5b06aeda
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63421161"
---
# <a name="expression-evaluator-implementation-strategy"></a>表达式计算器实施策略
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 快速创建的表达式计算器 (EE) 的一种方法是首先实现显示中的局部变量所需要的最小代码**局部变量**窗口。 最好要认识到，中的每一行**局部变量**窗口将显示名称、 类型和本地变量的值和所有三个由[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)对象。 可以从获取名称、 类型和本地变量的值`IDebugProperty2`对象通过调用其[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)方法。 详细了解如何显示中的局部变量**局部变量**窗口中，请参阅[显示局部变量](../../extensibility/debugger/displaying-locals.md)。  
  
## <a name="discussion"></a>讨论  
 可能的实现序列开头，实现[IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)。 [分析](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)并[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)方法需要实现以显示局部变量。 调用`IDebugExpressionEvaluator::GetMethodProperty`将返回`IDebugProperty2`对象，表示一种方法： 即[IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md)对象。 方法本身不会显示在**局部变量**窗口。  
  
 [EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)应下一步实现方法。 调试引擎 (DE) 调用此方法以获取本地变量和参数的列表，通过传递`IDebugProperty2::EnumChildren``guidFilter`自变量的`guidFilterLocalsPlusArgs`。 `IDebugProperty2::EnumChildren` 调用[EnumArguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)并[EnumLocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)，结合单个枚举中的结果。 请参阅[显示局部变量](../../extensibility/debugger/displaying-locals.md)的更多详细信息。  
  
## <a name="see-also"></a>请参阅  
 [实现表达式计算器](../../extensibility/debugger/implementing-an-expression-evaluator.md)   
 [显示局部](../../extensibility/debugger/displaying-locals.md)
