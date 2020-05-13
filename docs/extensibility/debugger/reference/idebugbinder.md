---
title: IDebugBinder |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder
helpviewer_keywords:
- IDebugBinder interface
ms.assetid: d1f31e5b-c6e2-4e02-8959-b3e86041b29c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fcdec19c4667356edaf9e057c86ddc24baf747b7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735972"
---
# <a name="idebugbinder"></a>IDebugBinder
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口将符号字段（通常由符号提供程序返回）绑定到包含符号当前值的内存上下文或对象。

## <a name="syntax"></a>语法

```
IDebugBinder : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 此接口支持表达式计算，必须由调试引擎 （DE） 实现。

## <a name="notes-for-callers"></a>呼叫者备注
 此接口用于表达式计算过程，通常用于[实现评估同步](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)和[评估Async](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugBinder`。

|方法|描述|
|------------|-----------------|
|[绑定](../../../extensibility/debugger/reference/idebugbinder-bind.md)|获取包含符号当前值的内存上下文或对象。|
|[ResolveRuntimeType](../../../extensibility/debugger/reference/idebugbinder-resolveruntimetype.md)|确定对象的运行时类型。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugbinder-getmemorycontext.md)|将对象位置或内存地址转换为内存上下文。|
|[GetFunctionObject](../../../extensibility/debugger/reference/idebugbinder-getfunctionobject.md)|获取用于创建函数参数的[IDebug函数对象](../../../extensibility/debugger/reference/idebugfunctionobject.md)。|
|[ResolveDynamicType](../../../extensibility/debugger/reference/idebugbinder-resolvedynamictype.md)|获取变量的确切类型。|

## <a name="remarks"></a>备注
 此接口返回表达式赋值器在解析树中使用的对象。 表达式赋值器通过使用符号提供程序将表达式中的符号转换为[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)的实例来解析表达式，IDebugField 根据其类型和在源代码中的位置来描述每个符号。 [绑定](../../../extensibility/debugger/reference/idebugbinder-bind.md)方法将`IDebugField`对象转换为[IDebugObject 对象](../../../extensibility/debugger/reference/idebugobject.md)，这些对象将符号类型连接或绑定到内存中的实际值。 然后`IDebugObject`，这些对象存储在解析树中，以供以后评估。

## <a name="requirements"></a>要求
 标题： ee.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
