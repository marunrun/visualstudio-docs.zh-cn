---
title: IDebugManagedObject::GetManagedObject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugManagedObject::GetManagedObject
helpviewer_keywords:
- IDebugManagedObject::GetManagedObject method
ms.assetid: 6abe1402-6aad-41e6-8ec1-ae12d5945992
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 75e0367aaddb28e2af2703904fd77b4e4f9f6322
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349395"
---
# <a name="idebugmanagedobjectgetmanagedobject"></a>IDebugManagedObject::GetManagedObject
返回表示托管的对象的接口。

## <a name="syntax"></a>语法

```cpp
HRESULT GetManagedObject( 
   IUnknown** ppManagedObject
);
```

```cpp
int GetManagedObject(
   out object ppManagedObject
);
```

## <a name="parameters"></a>参数
`ppManagedObject`\
[out]返回表示托管的对象的接口。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的接口可以查询由托管类，允许其调用的方法实现任何接口。

## <a name="see-also"></a>请参阅
- [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)