---
title: 显示局部 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, displaying locals
ms.assetid: 62264cec-845b-4233-aed7-0b038fa79250
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3a8a73fb8ab95602538be56f18834233dbad7132
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345791"
---
# <a name="display-locals"></a>显示局部变量
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 始终执行方法，也称为包含的方法或当前方法的上下文中发生。 当将暂停执行时，Visual Studio 调用的调试引擎 (DE) 若要获取本地变量的列表和参数，统称为该方法的局部变量。 Visual Studio 将显示这些局部变量和中的值进行**局部变量**窗口。

 若要显示局部变量，DE 调用[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)属于 EE 方法并为其提供评估上下文，即、 符号提供程序 (SP)、 当前执行地址和绑定器对象。 有关详细信息，请参阅[评估上下文](../../extensibility/debugger/evaluation-context.md)。 如果调用成功，`IDebugExpressionEvaluator::GetMethodProperty`方法将返回[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)对象，表示包含当前执行地址的方法。

 DE 调用[EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)若要获取[IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)对象，该筛选以返回唯一局部变量和枚举以生成一系列对象[DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)结构。 每个结构包含名称、 类型和局部变量的值。 类型和值以适合显示的格式化字符串形式存储。 名称、 类型和值通常一起显示在一行中**局部变量**窗口。

> [!NOTE]
> **快速监视**并**监视**窗口还显示具有相同的格式的名称、 值和类型的变量。 但是，通过调用获取这些值[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)而不是`IDebugProperty2::EnumChildren`。

## <a name="in-this-section"></a>本节内容
 [局部的实现示例](../../extensibility/debugger/sample-implementation-of-locals.md)使用示例逐步实现局部变量的过程。

## <a name="related-sections"></a>相关章节
 [评估上下文](../../extensibility/debugger/evaluation-context.md)说明当调试引擎 (DE) 调用表达式计算器 (EE) 时，它可以通过三个参数。

## <a name="see-also"></a>请参阅
 [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)