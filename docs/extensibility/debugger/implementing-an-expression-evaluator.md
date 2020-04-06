---
title: 实现表达式赋值器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
ms.assetid: e9ada7be-845e-4baa-bf8f-e4890e7ba490
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a8c7c9a1130794dd4c28f212afd6cb3c030f5a1b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738539"
---
# <a name="implement-an-expression-evaluator"></a>实现表达式赋值器
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 计算表达式是调试引擎 （DE）、符号提供程序 （SP）、活页夹对象和表达式赋值器 （EE） 之间的复杂相互作用。 这四个组件由一个组件实现并由另一个组件使用的接口连接。

 EE 以字符串的形式从 DE 获取表达式，并对其进行解析或计算。 EE 运行以下接口，DE 使用这些接口：

- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)

- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)

  EE 调用 DE 提供的活页夹对象，以获得符号和对象的值。 EE 使用以下接口，这些接口由 DE 实现：

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

- [IDebugArrayObject](../../extensibility/debugger/reference/idebugarrayobject.md)

- [IDebugFunctionObject](../../extensibility/debugger/reference/idebugfunctionobject.md)

- [IDebugPointerObject](../../extensibility/debugger/reference/idebugpointerobject.md)

- [IDebugManagedObject](../../extensibility/debugger/reference/idebugmanagedobject.md)

- [IEnumDebugObjects](../../extensibility/debugger/reference/ienumdebugobjects.md)

- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)

  EE 运行[IDebugproperty2](../../extensibility/debugger/reference/idebugproperty2.md)。 `IDebugProperty2`提供用于描述表达式计算结果的机制，例如局部变量、基元或 Visual Studio 的对象，然后该函数在 **"局部变量**"、**监视**或 **"立即"** 窗口中显示相应的信息。

  当 DE 要求提供信息时，它向 EE 授予该 SP。 SP 运行描述地址和字段的接口，例如以下接口及其衍生物：

- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)

- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)

- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)

  EE 会使用所有这些接口。

## <a name="in-this-section"></a>在本节中
 [表达式赋值器实现策略](../../extensibility/debugger/expression-evaluator-implementation-strategy.md)为表达式赋值器 （EE） 实施策略定义三步过程。

## <a name="see-also"></a>请参阅
- [编写 CLR 表达式赋值器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
