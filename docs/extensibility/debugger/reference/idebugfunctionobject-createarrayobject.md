---
title: IDebug函数对象：：创建ArrayObject |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateArrayObject
helpviewer_keywords:
- IDebugFunctionObject::CreateArrayObject method
ms.assetid: a380e53c-15f1-401f-927f-f366eea789e6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bd4c07f2b95ff3077de79d4bc63f4fad19b0c6fa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728614"
---
# <a name="idebugfunctionobjectcreatearrayobject"></a>IDebugFunctionObject::CreateArrayObject
创建数组对象。 此数组可以包含基元或对象实例值。

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
[在]指定[OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md)枚举中的值，指示新数组对象的类型。

`pClassField`\
[在]如果创建对象实例值数组，则表示对象的类的[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象。 如果创建基元对象的数组，则此参数为空值。

`dwRank`\
[在]数组的级别或维度数。

`dwDims`\
[在]数组的每个维度的大小。

`dwLowBounds`\
[在]每个维度（通常为 0 或 1）的原点。

`ppObject`\
[出]返回表示新创建的数组的[IDebugObject 对象](../../../extensibility/debugger/reference/idebugobject.md)。 这实际上是一个[IDebugArray 对象](../../../extensibility/debugger/reference/idebugarrayobject.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法以创建一个对象，该对象表示由[IDebug函数对象](../../../extensibility/debugger/reference/idebugfunctionobject.md)接口表示的函数的数组参数。

## <a name="see-also"></a>请参阅
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
