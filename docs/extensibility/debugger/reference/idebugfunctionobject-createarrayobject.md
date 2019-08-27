---
title: IDebugFunctionObject::CreateArrayObject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateArrayObject
helpviewer_keywords:
- IDebugFunctionObject::CreateArrayObject method
ms.assetid: a380e53c-15f1-401f-927f-f366eea789e6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f8d5f6ea8b33605c51fa88464b091ccd3714730d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352152"
---
# <a name="idebugfunctionobjectcreatearrayobject"></a>IDebugFunctionObject::CreateArrayObject
创建一个数组对象。 此数组可以包含任一基元或对象实例的值。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateArrayObject( 
   OBJECT_TYPE    ot,
   IDebugField*   pClassField,
   DWORD          dwRank,
   DWORD          dwDims[],
   DWORD          dwLowBounds[],
   IDebugObject** ppObject
);
```

```csharp
int CreateArrayObject(
   enum_OBJECT_TYPE ot,
   IDebugField      pClassField,
   uint             dwRank,
   uint[]           dwDims,
   uint[]           dwLowBounds,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>参数
`ot`\
[in]指定一个介于[OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md)枚举，指示新的数组对象的类型。

`pClassField`\
[in][IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象，表示对象的类，如果创建实例值的对象的数组。 如果创建基元对象的数组，此参数是一个 null 值。

`dwRank`\
[in]秩或维数的数组。

`dwDims`\
[in]每个维度的数组大小。

`dwLowBounds`\
[in]每个维度原点 （通常 0 或 1）。

`ppObject`\
[out]返回[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)对象，表示新创建的数组。 这实际上是[IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法以创建表示由表示该函数的数组参数的对象[IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)接口。

## <a name="see-also"></a>请参阅
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)