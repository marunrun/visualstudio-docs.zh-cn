---
title: IPropertyProxyEESide::InPlaceUpdateObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
helpviewer_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
ms.assetid: abf89411-1853-4f23-b244-d5e0afa197b1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6ce2826aa0bd75638d6f5ee8086cbcce96517ce7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329424"
---
# <a name="ipropertyproxyeesideinplaceupdateobject"></a>IPropertyProxyEESide::InPlaceUpdateObject
使用给定的数据对象中更新对象的数据，并返回新的数据对象，表示对象的新数据。

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
[in][IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)对象，其中包含新数据。

`dataOut`\
[out]返回一个新`IEEDataStorage`对象，其中包含被替换的数据。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 此方法实际上更新对象的数据。 在返回的数据[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)对象不需要为在传入的数据相同`IEEDataStorage`对象，但返回的对象必须反映该属性的当前值。

 EE 通常没有实现传入的数据对象。 但是，此方法返回的对象始终通过 EE，它允许 EE 实现实现`IEEDataStorage`上任何类所需的接口。

 [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)方法创建基于传入的数据对象的数据对象，但不会影响该属性的原始数据。

## <a name="see-also"></a>请参阅
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)