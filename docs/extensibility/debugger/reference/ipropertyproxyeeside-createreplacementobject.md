---
title: IPropertyProxyEEside：创建替换对象 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::CreateReplacementObject
helpviewer_keywords:
- IPropertyProxyEESide::CreateReplacementObject
ms.assetid: 0cfe79b8-c3f1-48b0-a225-e39dee2c92fe
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f449a505c56c180f1bab021007f1b635a2461996
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715042"
---
# <a name="ipropertyproxyeesidecreatereplacementobject"></a>IPropertyProxyEESide::CreateReplacementObject
创建特定于表达式赋值器 （EE） 的数据对象的副本。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateReplacementObject(
   IEEDataStorage*  dataIn,
   IEEDataStorage** dataOut
);
```

```csharp
int CreateReplacementObject(
   IEEDataStorage     dataIn,
   out IEEDataStorage dataOut
);
```

## <a name="parameters"></a>参数
`dataIn`\
[在]保存要复制数据的[IEEData 存储](../../../extensibility/debugger/reference/ieedatastorage.md)对象。

`dataOut`\
[出]返回新`IEEDataStorage`对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法被赋予一个[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)对象，表示字节数组。 此传入数据对象通常不由 EE 实现。 但是，此方法返回的对象始终由 EE 实现，它允许 EE 在所需的任何类上`IEEDataStorage`实现接口。

 请注意，传入`IEEDataStorage`对象提供的数据必须是传出`IEEDataStorage`对象中相同的数据。

## <a name="see-also"></a>请参阅
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
