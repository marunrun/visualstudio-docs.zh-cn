---
title: IProperty 代理边：原位更新对象 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714894"
---
# <a name="ipropertyproxyeesideinplaceupdateobject"></a>IPropertyProxyEESide::InPlaceUpdateObject
使用给定的数据对象更新对象的数据，并返回表示对象新数据的新数据对象。

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
[在]包含新[数据的 IEEData 存储](../../../extensibility/debugger/reference/ieedatastorage.md)对象。

`dataOut`\
[出]返回包含替换`IEEDataStorage`数据的新对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法实际上更新对象的数据。 返回的[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)对象中的数据不需要与传入`IEEDataStorage`对象中的数据相同，但返回的对象必须反映属性的当前值。

 传入数据对象通常不由 EE 实现。 但是，此方法返回的对象始终由 EE 实现，它允许 EE 在所需的任何类上`IEEDataStorage`实现接口。

 [Create替换对象](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)方法基于传入数据对象创建数据对象，但不会影响属性的原始数据。

## <a name="see-also"></a>请参阅
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)
