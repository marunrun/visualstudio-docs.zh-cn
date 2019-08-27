---
title: IDebugFunctionObject::CreateArrayObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateArrayObject
helpviewer_keywords:
- IDebugFunctionObject::CreateArrayObject method
ms.assetid: a380e53c-15f1-401f-927f-f366eea789e6
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 53c1961eb1ed72580fc314d7a1542ddc926780f9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205812"
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

#### <a name="parameters"></a>Parameters
 `ot`

 [in]指定一个介于[OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md)枚举，指示新的数组对象的类型。

 `pClassField`

 [in][IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象，表示对象的类，如果创建实例值的对象的数组。 如果创建基元对象的数组，此参数是一个 null 值。

 `dwRank`

 [in]秩或维数的数组。

 `dwDims`

 [in]每个维度的数组大小。

 `dwLowBounds`

 [in]每个维度原点 （通常 0 或 1）。

 `ppObject`

 [out]返回[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)对象，表示新创建的数组。 这实际上是[IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法以创建表示由表示该函数的数组参数的对象[IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)接口。

## <a name="see-also"></a>请参阅
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)