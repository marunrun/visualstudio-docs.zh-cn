---
title: IDebugFunctionObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject
helpviewer_keywords:
- IDebugFunctionObject interface
ms.assetid: 8d94e97c-a9d1-400c-8a98-a44b5385b33a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6433c1f2c540b040a3b3beccc264377e69592387
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80728498"
---
# <a name="idebugfunctionobject"></a>IDebugFunctionObject
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示一个函数。

## <a name="syntax"></a>语法

```
IDebugFunctionObject : IDebugObject
```

## <a name="notes-for-implementers"></a>实施者注意事项
 表达式计算器实现此接口来表示函数。

## <a name="notes-for-callers"></a>调用方说明
 此接口是 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 接口的专用化，使用接口上的 [QueryInterface](/cpp/atl/queryinterface) 获得 `IDebugObject` 。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了从 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)继承的方法之外，接口还 `IDebugFunctionObject` 公开以下方法。

|方法|说明|
|------------|-----------------|
|[CreatePrimitiveObject](../../../extensibility/debugger/reference/idebugfunctionobject-createprimitiveobject.md)|创建基元数据对象。|
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject-createobject.md)|使用构造函数创建对象。|
|[CreateObjectNoConstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)|创建不包含构造函数的对象。|
|[CreateArrayObject](../../../extensibility/debugger/reference/idebugfunctionobject-createarrayobject.md)|创建数组对象。|
|[CreateStringObject](../../../extensibility/debugger/reference/idebugfunctionobject-createstringobject.md)|创建一个字符串对象。|
|[评估](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)|调用函数并将生成的值作为对象返回。|

## <a name="remarks"></a>备注
 此接口使表达式计算器可以在分析树中表示函数。 `Create`此接口中的方法用于构造对象，这些对象表示方法的输入参数。 然后，可以通过调用 [计算](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md) 方法来执行该函数，该方法返回表示函数返回值的对象。

## <a name="requirements"></a>要求
 标头： ee。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
