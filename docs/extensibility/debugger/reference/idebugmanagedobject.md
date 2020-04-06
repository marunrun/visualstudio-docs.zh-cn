---
title: IDebug托管对象 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugManagedObject
helpviewer_keywords:
- IDebugManagedObject interface
ms.assetid: 3ae09d34-112c-4285-80ee-9f7f8dc414d7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6fbd270aa1b65f05f308d41d22f154fb53b8833d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727690"
---
# <a name="idebugmanagedobject"></a>IDebugManagedObject
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口使表达式赋值器 （EE） 能够调用值类实例的属性或方法（例如`System.Decimal`），并在不调用正在调试的程序上的[评估](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)的情况下设置其值。

## <a name="syntax"></a>语法

```
IDebugManagedObject : IDebugObject
```

## <a name="notes-for-implementers"></a>实施者说明
 表达式赋值器实现此接口以表示托管代码对象（如变量）。

## <a name="notes-for-callers"></a>呼叫者备注
 要获取此接口，请调用表示值类实例的[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)上的[Get托管调试对象](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了从[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)继承的方法外，`IDebugManagedObject`接口还公开了以下方法。

|方法|描述|
|------------|-----------------|
|[GetManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-getmanagedobject.md)|返回表示托管代码对象的接口，并从中获取任何适当的托管代码接口。|
|[SetFromManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-setfrommanagedobject.md)|将此对象的值设置为指定的托管代码对象的值。|

## <a name="remarks"></a>备注
 表达式赋值器使用此接口将托管代码对象存储在解析树中。

## <a name="requirements"></a>要求
 标题： ee.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [评估](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)
