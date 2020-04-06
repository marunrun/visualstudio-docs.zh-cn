---
title: 局部变量的样本实施 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], local variables
- expression evaluation, local variables
ms.assetid: 66a2e00a-f558-4e87-96b8-5ecf5509e04c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6b70e0f9091d40ed6b5fc44934606f42ccd84b21
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713072"
---
# <a name="sample-implementation-of-locals"></a>局部变量的样本实现
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 以下是 Visual Studio 如何从表达式赋值器 （EE） 获取方法的局部变量的概述：

1. Visual Studio 调用调试引擎的 （DE） [GetDebugProperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)获取[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)对象，该对象表示堆栈帧的所有属性，包括局部变量。

2. `IDebugStackFrame2::GetDebugProperty`调用[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)获取描述断点发生方法的对象。 DE 提供符号提供程序 （[IDebugSymbolProvider），](../../extensibility/debugger/reference/idebugsymbolprovider.md)地址 （[IDebugAddress）](../../extensibility/debugger/reference/idebugaddress.md)和活页夹 （[IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)）.

3. `IDebugExpressionEvaluator::GetMethodProperty`使用提供`IDebugAddress`的对象调用[GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)以获取表示包含指定地址的方法的[IDebugContainerField。](../../extensibility/debugger/reference/idebugcontainerfield.md)

4. 查询`IDebugContainerField` [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md)接口的接口。 正是这个接口提供了对方法的局部变量的访问。

5. `IDebugExpressionEvaluator::GetMethodProperty`实例化运行`IDebugProperty2`接口以表示方法的`CFieldProperty`局部变量的类（在示例中调用）。 对象`IDebugMethodField``CFieldProperty`与`IDebugSymbolProvider`、`IDebugAddress`和`IDebugBinder`对象一起放置在此对象中。

6. 初始化`CFieldProperty`对象时，`IDebugMethodField`在对象上调用[GetInfo](../../extensibility/debugger/reference/idebugfield-getinfo.md)以获取有关方法本身的所有可显示信息[FIELD_INFO](../../extensibility/debugger/reference/field-info.md)结构。

7. `IDebugExpressionEvaluator::GetMethodProperty`将`CFieldProperty`对象作为对象返回`IDebugProperty2`。

8. Visual Studio 使用筛选器在返回`IDebugProperty2`的对象上调用[Enum 儿童](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)，该筛选器`guidFilterLocalsPlusArgs`返回包含该方法的局部变量的[IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)对象。 此枚举通过调用[枚举本地变量](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)和[枚举参数](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)来填充。

9. 可视化工作室调用[下一个](../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md)获取每个本地[DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)结构。 此结构包含指向本地`IDebugProperty2`接口的指针。

10. Visual Studio 为每个本地调用[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)以获取本地名称、值和类型。 此信息将显示在 **"局部变量"** 窗口中。

## <a name="in-this-section"></a>在本节中
 [实现 GetMethod 属性](../../extensibility/debugger/implementing-getmethodproperty.md)描述[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)的实现。

 [枚举局部变量](../../extensibility/debugger/enumerating-locals.md)描述调试引擎 （DE） 如何调用枚举本地变量或参数。

 [获取本地属性](../../extensibility/debugger/getting-local-properties.md)描述 DE 如何调用以获取一个或多个局部变量的名称、类型和值。

 [获取本地值](../../extensibility/debugger/getting-local-values.md)讨论获取本地值，这需要计算上下文提供的活页夹对象的服务。

 [评估本地人](../../extensibility/debugger/evaluating-locals.md)解释如何评估局部变量。

## <a name="related-sections"></a>相关章节
 [评估上下文](../../extensibility/debugger/evaluation-context.md)提供 DE 调用表达式赋值器 （EE） 时传递的参数。

 [MyCEE 样本](https://msdn.microsoft.com/library/624a018b-9179-402f-9d48-3aec87b48f4f)演示为 MyC 语言创建表达式赋值器的一种实现方法。

## <a name="see-also"></a>请参阅
- [显示本地变量](../../extensibility/debugger/displaying-locals.md)
