---
title: IPropertyProxyEESide::InitSourceDataProvider |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::InitSourceDataProvider
helpviewer_keywords:
- IPropertyProxyEESide::InitSourceDataProvider
ms.assetid: 5156f593-5052-4e3a-9d02-081916fb342d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 725ac07c85dd31edaf97200a7a8668ff3efd9ab9
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329527"
---
# <a name="ipropertyproxyeesideinitsourcedataprovider"></a>IPropertyProxyEESide::InitSourceDataProvider
初始化此对象的源数据并返回一个包含初始数据的对象。

## <a name="syntax"></a>语法

```cpp
HRESULT InitSourceDataProvider(
   IEEDataStorage** dataOut
);
```

```csharp
int InitSourceDataProvider(
   out IEEDataStorage dataOut
);
```

## <a name="parameters"></a>参数
`dataOut`\
[out]返回[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)对象

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 此方法会执行任何所需初始化对象，以便它可以返回[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)上对象的数据的接口。 这允许查看和，如果允许，更改类型可视化工具对象的数据。

## <a name="see-also"></a>请参阅
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)