---
title: IDebug函数对象 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728498"
---
# <a name="idebugfunctionobject"></a>IDebugFunctionObject
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示函数。

## <a name="syntax"></a>语法

```
IDebugFunctionObject : IDebugObject
```

## <a name="notes-for-implementers"></a>实施者说明
 表达式赋值器实现此接口以表示函数。

## <a name="notes-for-callers"></a>呼叫者备注
 此接口是[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口的专门化，使用接口上的`IDebugObject`[查询接口](/cpp/atl/queryinterface)获得。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了从[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)继承的方法外，`IDebugFunctionObject`接口还公开了以下方法。

|方法|描述|
|------------|-----------------|
|[CreatePrimitiveObject](../../../extensibility/debugger/reference/idebugfunctionobject-createprimitiveobject.md)|创建基元数据对象。|
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject-createobject.md)|使用构造函数创建对象。|
|[CreateObjectNoConstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)|创建没有构造函数的对象。|
|[CreateArrayObject](../../../extensibility/debugger/reference/idebugfunctionobject-createarrayobject.md)|创建数组对象。|
|[CreateStringObject](../../../extensibility/debugger/reference/idebugfunctionobject-createstringobject.md)|创建字符串对象。|
|[评估](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)|调用函数并将结果值作为对象返回。|

## <a name="remarks"></a>备注
 此接口使表达式赋值器能够表示解析树中的函数。 此`Create`接口中的方法用于构造表示方法的输入参数的对象。 然后，可以通过调用[评估](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)方法来执行该函数，该方法返回表示函数返回值的对象。

## <a name="requirements"></a>要求
 标题： ee.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
