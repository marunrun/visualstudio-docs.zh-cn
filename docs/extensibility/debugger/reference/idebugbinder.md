---
title: IDebugBinder |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80735972"
---
# <a name="idebugbinder"></a>IDebugBinder
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口将符号字段（通常由符号提供程序返回）绑定到包含符号当前值的内存上下文或对象。

## <a name="syntax"></a>语法

```
IDebugBinder : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 此接口支持表达式计算，必须由调试引擎实现 (DE) 。

## <a name="notes-for-callers"></a>调用方说明
 此接口在表达式计算过程中使用，通常用于 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 和 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)的实现。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugBinder` 。

|方法|说明|
|------------|-----------------|
|[绑定](../../../extensibility/debugger/reference/idebugbinder-bind.md)|获取包含符号当前值的内存上下文或对象。|
|[ResolveRuntimeType](../../../extensibility/debugger/reference/idebugbinder-resolveruntimetype.md)|确定对象的运行时类型。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugbinder-getmemorycontext.md)|将对象位置或内存地址转换为内存上下文。|
|[GetFunctionObject](../../../extensibility/debugger/reference/idebugbinder-getfunctionobject.md)|获取用于创建函数参数的 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 对象。|
|[ResolveDynamicType](../../../extensibility/debugger/reference/idebugbinder-resolvedynamictype.md)|获取变量的确切类型。|

## <a name="remarks"></a>备注
 此接口返回分析树中的表达式计算器使用的对象。 表达式计算器通过使用符号提供程序将表达式中的符号转换为 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)的实例，以将其类型和位置描述为在源代码中。 [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)方法将 `IDebugField` 对象转换为[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)对象，这些对象将符号类型连接或绑定到内存中的实际值。 然后，将这些 `IDebugObject` 对象存储在分析树中以便以后进行计算。

## <a name="requirements"></a>要求
 标头： ee。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
