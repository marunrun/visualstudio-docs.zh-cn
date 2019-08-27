---
title: IDebugFunctionObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject
helpviewer_keywords:
- IDebugFunctionObject interface
ms.assetid: 8d94e97c-a9d1-400c-8a98-a44b5385b33a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5fb0d969268e7765abe5c3ebdc9fc000a10a3aa0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66313441"
---
# <a name="idebugfunctionobject"></a>IDebugFunctionObject
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示的函数。

## <a name="syntax"></a>语法

```
IDebugFunctionObject : IDebugObject
```

## <a name="notes-for-implementers"></a>实施者的说明
 表达式计算器实现此接口来表示一个函数。

## <a name="notes-for-callers"></a>调用方的说明
 此接口是专用化[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口，并使用获取[QueryInterface](/cpp/atl/queryinterface)上`IDebugObject`接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了继承的方法之外[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)，则`IDebugFunctionObject`接口公开以下方法。

|方法|描述|
|------------|-----------------|
|[CreatePrimitiveObject](../../../extensibility/debugger/reference/idebugfunctionobject-createprimitiveobject.md)|创建一个基元数据对象。|
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject-createobject.md)|创建使用构造函数的对象。|
|[CreateObjectNoConstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)|使用没有构造函数创建的对象。|
|[CreateArrayObject](../../../extensibility/debugger/reference/idebugfunctionobject-createarrayobject.md)|创建一个数组对象。|
|[CreateStringObject](../../../extensibility/debugger/reference/idebugfunctionobject-createstringobject.md)|创建一个字符串对象。|
|[Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)|调用函数，并返回结果值作为对象。|

## <a name="remarks"></a>备注
 此接口使表达式计算器来表示分析树中的函数。 `Create`此接口中的方法用于构造对象表示的输入的参数的方法。 然后可以通过调用执行函数[Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)方法，它将返回一个表示该函数的返回值的对象。

## <a name="requirements"></a>要求
 标头： ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)