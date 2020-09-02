---
title: 局部变量的示例实现 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], local variables
- expression evaluation, local variables
ms.assetid: 66a2e00a-f558-4e87-96b8-5ecf5509e04c
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6e943fd7ba27fe21029bab4d818803186147476e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704891"
---
# <a name="sample-implementation-of-locals"></a>局部的实现示例
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 下面概述了 Visual Studio 如何从表达式计算器获取方法的局部变量 (EE) ：  
  
1. Visual Studio 将调用调试引擎的 (DE) [GetDebugProperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) 获取一个 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 对象，该对象表示堆栈帧的所有属性，包括局部变量。  
  
2. `IDebugStackFrame2::GetDebugProperty` 调用 [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) 以获取一个对象，该对象描述发生断点的方法。 DE 提供了一个符号提供程序 ([IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)) 、地址 ([IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)) 和一个活页夹 ([IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)) 。  
  
3. `IDebugExpressionEvaluator::GetMethodProperty` 使用提供的对象调用 [GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md) `IDebugAddress` ，以获取 [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) ，该对象表示包含指定地址的方法。  
  
4. 为 `IDebugContainerField` [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) 接口查询接口。 此接口可用于访问方法的局部变量。  
  
5. `IDebugExpressionEvaluator::GetMethodProperty` 实例化一个类 (`CFieldProperty` 在示例) 中调用，该类实现 `IDebugProperty2` 接口以表示该方法的局部变量。 `IDebugMethodField`对象 `CFieldProperty` 与 `IDebugSymbolProvider` 、 `IDebugAddress` 和对象一起放置在此对象中 `IDebugBinder` 。  
  
6. `CFieldProperty`初始化对象时，将对对象调用[GetInfo](../../extensibility/debugger/reference/idebugfield-getinfo.md) ， `IDebugMethodField` 以获取包含有关该方法自身的所有可显示信息的[FIELD_INFO](../../extensibility/debugger/reference/field-info.md)结构。  
  
7. `IDebugExpressionEvaluator::GetMethodProperty``CFieldProperty`以对象的形式返回对象 `IDebugProperty2` 。  
  
8. Visual Studio 将对返回的对象调用 [EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) ， `IDebugProperty2` 并返回筛选器 `guidFilterLocalsPlusArgs` 。 这会返回一个包含该方法的局部变量的 [IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) 对象。 此枚举由对 [EnumLocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) 和 [EnumArguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)的调用填充。  
  
9. Visual Studio 调用 " [下一步](../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md) " 以获取每个本地的 [DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md) 结构。 此结构包含指向 `IDebugProperty2` 本地接口的指针。  
  
10. Visual Studio 为每个本地调用 [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) ，以获取本地的名称、值和类型。 这是在 " **局部变量** " 窗口中显示的信息。  
  
## <a name="in-this-section"></a>本节内容  
 [实现 GetMethodProperty](../../extensibility/debugger/implementing-getmethodproperty.md)  
 介绍 [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)的实现。  
  
 [枚举局部](../../extensibility/debugger/enumerating-locals.md)  
 描述调试引擎 (如何) 进行调用以枚举局部变量或自变量。  
  
 [获取局部属性](../../extensibility/debugger/getting-local-properties.md)  
 介绍如何进行调用以获取一个或多个局部变量的名称、类型和值。  
  
 [获取局部值](../../extensibility/debugger/getting-local-values.md)  
 讨论如何获取本地的值，它需要由计算上下文提供的联编程序对象的服务。  
  
 [计算局部](../../extensibility/debugger/evaluating-locals.md)  
 说明如何计算局部变量。  
  
## <a name="related-sections"></a>相关章节  
 [计算上下文](../../extensibility/debugger/evaluation-context.md)  
 提供在 DE 调用表达式计算器 (EE) 时传递的参数。  
  
 [MyCEE 示例](https://msdn.microsoft.com/624a018b-9179-402f-9d48-3aec87b48f4f)  
 演示一种实现方法，用于创建 MyC 语言的表达式计算器。  
  
## <a name="see-also"></a>另请参阅  
 [显示局部](../../extensibility/debugger/displaying-locals.md)
