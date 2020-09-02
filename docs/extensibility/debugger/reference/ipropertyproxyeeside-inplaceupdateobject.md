---
title: IPropertyProxyEESide：： InPlaceUpdateObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
helpviewer_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
ms.assetid: abf89411-1853-4f23-b244-d5e0afa197b1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 79167b0f7e8094fabf80bb9b2d83c94ac874aa31
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80714894"
---
# <a name="ipropertyproxyeesideinplaceupdateobject"></a>IPropertyProxyEESide::InPlaceUpdateObject
使用给定的数据对象更新对象的数据，并返回一个表示该对象的新数据的新数据对象。

## <a name="syntax"></a>语法

```cpp
HRESULT InPlaceUpdateObject(
   [in] IEEDataStorage*   dataIn,
   [out] IEEDataStorage** dataOut
);
```

```csharp
int InPlaceUpdateObject(
   IEEDataStorage     dataIn,
   out IEEDataStorage dataOut
);
```

## <a name="parameters"></a>参数
`dataIn`\
中一个包含新数据的 [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) 对象。

`dataOut`\
弄返回一个新 `IEEDataStorage` 的对象，其中包含被替换的数据。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 此方法实际更新对象的数据。 返回的 [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) 对象中的数据不需要与传入对象中的数据相同 `IEEDataStorage` ，但返回的对象必须反映属性的当前值。

 输入的数据对象通常不是由 EE 实现的。 但是，此方法返回的对象始终由 EE 实现，这使 EE 可以 `IEEDataStorage` 在所需的任何类上实现接口。

 [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)方法基于传入数据对象创建一个数据对象，但不会影响该属性的原始数据。

## <a name="see-also"></a>另请参阅
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)
