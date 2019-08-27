---
title: IDebugObject::IsEqual | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::IsEqual
helpviewer_keywords:
- IDebugObject::IsEqual method
ms.assetid: 4b76e663-ef2e-41ff-9be1-bf26d666a34a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cf592fa83a18c47bf676b84073c0be0e4cb476e8
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323589"
---
# <a name="idebugobjectisequal"></a>IDebugObject::IsEqual
将与此对象的对象进行比较。

## <a name="syntax"></a>语法

```cpp
HRESULT IsEqual( 
   IDebugObject* pObject,
   BOOL*         pfIsEqual
);
```

```csharp
int IsEqual(
   IDebugObject pObject,
   out int      pfIsEqual
);
```

## <a name="parameters"></a>参数
`pObject`\
[in][IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)对象，表示要比较的对象。

`pfIsEqual`\
[out]返回非零值 (`TRUE`) 的对象的值是相等; 否则为如果返回零 (`FALSE`)。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 通常情况下，此方法可以比较所表示的值的地址`pObject`参数，这[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)对象; 如果地址相等，则对象可被视为相等。

## <a name="see-also"></a>请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)