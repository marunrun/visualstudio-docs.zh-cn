---
title: IDebugBinder | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder
helpviewer_keywords:
- IDebugBinder interface
ms.assetid: d1f31e5b-c6e2-4e02-8959-b3e86041b29c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bdcc5e9cc87bbe97a1ff9092e34c73b72274d775
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66344342"
---
# <a name="idebugbinder"></a>IDebugBinder
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口将绑定符号字段，通常由符号提供程序，到内存上下文或对象，其中包含符号的当前值返回。

## <a name="syntax"></a>语法

```
IDebugBinder : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 此接口支持表达式计算，必须实现的调试引擎 (DE)。

## <a name="notes-for-callers"></a>调用方的说明
 此接口用于表达式计算的过程中，通常使用的实现中[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)并[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugBinder`。

|方法|描述|
|------------|-----------------|
|[Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)|获取内存上下文或对象，其中包含符号的当前值。|
|[ResolveRuntimeType](../../../extensibility/debugger/reference/idebugbinder-resolveruntimetype.md)|确定对象的运行时类型。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugbinder-getmemorycontext.md)|将对象位置或内存地址转换为内存上下文。|
|[GetFunctionObject](../../../extensibility/debugger/reference/idebugbinder-getfunctionobject.md)|获取[IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)对象，用于创建函数的参数。|
|[ResolveDynamicType](../../../extensibility/debugger/reference/idebugbinder-resolvedynamictype.md)|获取变量的确切类型。|

## <a name="remarks"></a>备注
 此接口返回表达式计算器使用的对象的分析树。 表达式计算器分析表达式使用符号提供程序将在表达式中的符号转换为的实例[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)，描述其类型和位置的源代码中根据每个符号。 [绑定](../../../extensibility/debugger/reference/idebugbinder-bind.md)方法将`IDebugField`对象添加到[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)在内存中的实际值类型对象的连接或绑定一个符号。 这些`IDebugObject`对象然后存储在更高版本评估的分析树。

## <a name="requirements"></a>要求
 标头： ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)