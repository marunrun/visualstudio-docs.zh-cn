---
title: 显示局部变量 |Microsoft Docs
description: 了解局部变量和参数的列表（统称为方法的局部变量），该方法在执行暂停时显示。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, displaying locals
ms.assetid: 62264cec-845b-4233-aed7-0b038fa79250
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ddc7bc564e4e294144eeb3fa34db8bdf73971053
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "96915539"
---
# <a name="display-locals"></a>显示局部变量
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 执行始终发生在方法（也称为包含方法或当前方法）的上下文中。 当执行暂停时，Visual Studio 将调用调试引擎 (DE) 以获取局部变量和参数的列表，统称为方法的局部变量。 Visual Studio 会在 " **局部变量** " 窗口中显示这些局部变量及其值。

 若要显示局部变量，则 DE 会调用属于 EE 的 [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) 方法，并为其提供一个计算上下文，即 (SP) 的符号提供程序、当前的执行地址和一个联编程序对象。 有关详细信息，请参阅 [计算上下文](../../extensibility/debugger/evaluation-context.md)。 如果调用成功，则 `IDebugExpressionEvaluator::GetMethodProperty` 方法返回一个 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 对象，该对象表示包含当前执行地址的方法。

 DE 调用 [EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) 来获取 [IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) 对象，该对象经过筛选后只返回局部变量并进行枚举，以生成 [DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md) 结构的列表。 每个结构都包含本地的名称、类型和值。 类型和值存储为适用于显示的格式化字符串。 名称、类型和值通常显示在 " **局部变量** " 窗口的一行中。

> [!NOTE]
> " **快速监视** " 和 " **监视** " 窗口还显示具有相同格式的名称、值和类型的变量。 不过，这些值通过调用 [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) 而不是获得 `IDebugProperty2::EnumChildren` 。

## <a name="in-this-section"></a>在本节中
 [局部变量的示例实现](../../extensibility/debugger/sample-implementation-of-locals.md) 使用示例逐步完成实现局部变量的过程。

## <a name="related-sections"></a>相关章节
 [计算上下文](../../extensibility/debugger/evaluation-context.md) 说明当调试引擎 (DE) 调用表达式计算器 (EE) 时，它将传递三个参数。

## <a name="see-also"></a>另请参阅
 [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
