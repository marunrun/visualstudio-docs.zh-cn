---
title: 实现表达式计算器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
ms.assetid: e9ada7be-845e-4baa-bf8f-e4890e7ba490
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 66a1a0cb78036982923d20e39a3a4c32b288e459
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66326191"
---
# <a name="implement-an-expression-evaluator"></a>实现表达式计算器
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 计算表达式是复杂叠加而调试引擎 (DE)、 符号提供程序 (SP)、 联编程序对象和表达式计算器 (EE) 之间。 以下四个组件的接口是由一个组件实现和使用由另一个连接。

 EE DE 中字符串的形式从所需的表达式和解析或对其进行计算。 EE 运行由德国的以下接口：

- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)

- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)

  EE 调用 DE，若要获取的符号和对象的值由提供的联编程序对象。 EE 使用由 DE 实现以下接口：

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

- [IDebugArrayObject](../../extensibility/debugger/reference/idebugarrayobject.md)

- [IDebugFunctionObject](../../extensibility/debugger/reference/idebugfunctionobject.md)

- [IDebugPointerObject](../../extensibility/debugger/reference/idebugpointerobject.md)

- [IDebugManagedObject](../../extensibility/debugger/reference/idebugmanagedobject.md)

- [IEnumDebugObjects](../../extensibility/debugger/reference/ienumdebugobjects.md)

- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)

  运行 EE [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)。 `IDebugProperty2` 提供用于描述结果的表达式计算，如本地变量、 基元或到 Visual Studio，然后显示中的相应信息的对象的机制**局部变量**，**监视**，或**即时**窗口。

  SP 时为指定 EE DE 通过要求提供的信息。 SP 运行描述地址和域，如下面的接口和其派生类的接口：

- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)

- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)

- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)

  EE 使用所有这些接口。

## <a name="in-this-section"></a>本节内容
 [表达式计算器实施策略](../../extensibility/debugger/expression-evaluator-implementation-strategy.md)定义了表达式计算器 (EE) 实施策略一个三步骤过程。

## <a name="see-also"></a>请参阅
- [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)