---
title: 显示本地变量 |微软文档
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
ms.openlocfilehash: 4d44b276aeb9c6acb0ef34cc186662d49246de7d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738929"
---
# <a name="display-locals"></a>显示局部变量
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 执行始终发生在方法的上下文中，也称为包含方法或当前方法。 当执行暂停时，Visual Studio 调用调试引擎 （DE） 来获取本地变量和参数的列表，统称为方法的局部变量。 可视化工作室在 **"局部变量"** 窗口中显示这些局部变量及其值。

 要显示局部变量，DE 调用属于 EE 的[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)方法，并给它一个评估上下文，即符号提供程序 （SP）、当前执行地址和活页夹对象。 有关详细信息，请参阅[评估上下文](../../extensibility/debugger/evaluation-context.md)。 如果调用成功，`IDebugExpressionEvaluator::GetMethodProperty`该方法将返回[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)对象，该对象表示包含当前执行地址的方法。

 DE 调用[Enum 儿童](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)获取[IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)对象，该对象经过筛选以仅返回局部变量并枚举以生成[DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)结构的列表。 每个结构都包含本地的名称、类型和值。 类型和值存储为格式化字符串，适合显示。 名称、类型和值通常一起显示在 **"局部变量"** 窗口的一行中。

> [!NOTE]
> **"快速监视**"和 **"监视"** 窗口还显示名称、值和类型格式相同的变量。 但是，这些值是通过调用[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)而不是`IDebugProperty2::EnumChildren`获得。

## <a name="in-this-section"></a>在本节中
 [局部变量的样本实现](../../extensibility/debugger/sample-implementation-of-locals.md)使用示例逐步完成本地变量的实现过程。

## <a name="related-sections"></a>相关章节
 [评估上下文](../../extensibility/debugger/evaluation-context.md)说明当调试引擎 （DE） 调用表达式赋值器 （EE） 时，它将传递三个参数。

## <a name="see-also"></a>请参阅
 [编写 CLR 表达式赋值器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
