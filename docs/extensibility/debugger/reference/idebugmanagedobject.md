---
title: IDebugManagedObject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugManagedObject
helpviewer_keywords:
- IDebugManagedObject interface
ms.assetid: 3ae09d34-112c-4285-80ee-9f7f8dc414d7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6744ae98a0210a6832bce1bdb0cd68f08145f3eb
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349419"
---
# <a name="idebugmanagedobject"></a>IDebugManagedObject
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口允许表达式计算器 (EE) 值类实例上调用属性或方法 (例如， `System.Decimal`)，并设置其值而无需调用[评估](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)上正在调试的程序。

## <a name="syntax"></a>语法

```
IDebugManagedObject : IDebugObject
```

## <a name="notes-for-implementers"></a>实施者的说明
 表达式计算器实现此接口来表示一个托管的代码对象，如变量。

## <a name="notes-for-callers"></a>调用方的说明
 若要获取此接口，请调用[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)上[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) ，表示值类的实例。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了继承的方法之外[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)，则`IDebugManagedObject`接口公开以下方法。

|方法|描述|
|------------|-----------------|
|[GetManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-getmanagedobject.md)|返回表示托管的代码对象，可以从任何哪些适当的托管代码中获得接口的接口。|
|[SetFromManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-setfrommanagedobject.md)|此对象的值设置为指定的托管的代码对象的值。|

## <a name="remarks"></a>备注
 表达式计算器使用此接口以托管的代码对象存储在分析树。

## <a name="requirements"></a>要求
 标头： ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)