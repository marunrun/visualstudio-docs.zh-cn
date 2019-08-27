---
title: 示例局部的实现 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], local variables
- expression evaluation, local variables
ms.assetid: 66a2e00a-f558-4e87-96b8-5ecf5509e04c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4c65ed0e3def028e710255d08ee1fe40080bfde5
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66315020"
---
# <a name="sample-implementation-of-locals"></a>局部的实现示例
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 下面是概述如何 Visual Studio 获取局部变量的方法从表达式计算器 (EE):

1. Visual Studio 会调用调试引擎 (DE) [GetDebugProperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)若要获取[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)对象，表示堆栈帧，其中包括局部变量的所有属性。

2. `IDebugStackFrame2::GetDebugProperty` 调用[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)获取一个对象，描述在其中发生断点的方法。 DE 提供符号提供程序 ([IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md))，一个地址 ([IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md))，和联编程序 ([IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md))。

3. `IDebugExpressionEvaluator::GetMethodProperty` 调用[GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)与所提供`IDebugAddress`对象，以获取[IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) ，表示包含指定的地址的方法。

4. `IDebugContainerField`接口中查询[IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md)接口。 此接口，该方法的局部变量可以访问它。

5. `IDebugExpressionEvaluator::GetMethodProperty` 实例化一个类 (称为`CFieldProperty`示例中) 运行一次`IDebugProperty2`接口来表示该方法的局部变量。 `IDebugMethodField`的对象置于这`CFieldProperty`对象连同`IDebugSymbolProvider`， `IDebugAddress`，和`IDebugBinder`对象。

6. 当`CFieldProperty`初始化对象时， [GetInfo](../../extensibility/debugger/reference/idebugfield-getinfo.md)上调用`IDebugMethodField`对象获取[FIELD_INFO](../../extensibility/debugger/reference/field-info.md)结构，其中包含有关该方法本身的所有可显示信息。

7. `IDebugExpressionEvaluator::GetMethodProperty` 返回`CFieldProperty`对象作为`IDebugProperty2`对象。

8. Visual Studio 调用[EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)对返回`IDebugProperty2`对象与筛选器`guidFilterLocalsPlusArgs`，它将返回[IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)对象，它包含方法的局部变量。 此枚举通过调用来填充[EnumLocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)并[EnumArguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)。

9. Visual Studio 调用[下一步](../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md)来获取[DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)每个本地的结构。 此结构包含一个指向`IDebugProperty2`本地接口。

10. Visual Studio 调用[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)对于每个本地获取的本地名称、 值和类型。 此信息显示在**局部变量**窗口。

## <a name="in-this-section"></a>本节内容
 [实现 GetMethodProperty](../../extensibility/debugger/implementing-getmethodproperty.md)介绍的实现[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)。

 [枚举局部变量](../../extensibility/debugger/enumerating-locals.md)描述如何调试引擎 (DE) 进行调用以枚举本地变量或参数。

 [获取本地属性](../../extensibility/debugger/getting-local-properties.md)介绍 DE 如何通过调用来获取名称、 类型和一个或多个局部变量的值。

 [获取本地值](../../extensibility/debugger/getting-local-values.md)讨论获取本地，需要通过评估上下文提供的联编程序对象的服务的值。

 [评估局部变量](../../extensibility/debugger/evaluating-locals.md)介绍了如何计算局部变量。

## <a name="related-sections"></a>相关章节
 [评估上下文](../../extensibility/debugger/evaluation-context.md)提供 DE 调用表达式计算器 (EE) 时传递的参数。

 [MyCEE 示例](https://msdn.microsoft.com/library/624a018b-9179-402f-9d48-3aec87b48f4f)演示一个实现方法创建 MyC 语言的表达式计算器。

## <a name="see-also"></a>请参阅
- [显示局部](../../extensibility/debugger/displaying-locals.md)