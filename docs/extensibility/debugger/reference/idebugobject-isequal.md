---
title: IDebugObject：：是平等的 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::IsEqual
helpviewer_keywords:
- IDebugObject::IsEqual method
ms.assetid: 4b76e663-ef2e-41ff-9be1-bf26d666a34a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 13018e31fb5f8bed89a0a290d687360a605a855d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726499"
---
# <a name="idebugobjectisequal"></a>IDebugObject::IsEqual
将对象与此对象进行比较。

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
[在]表示要与之比较的对象的[IDebugObject 对象](../../../extensibility/debugger/reference/idebugobject.md)。

`pfIsEqual`\
[出]如果对象的值相等，`TRUE`则返回非零 （ ），否则，返回零`FALSE`（）。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 通常，此方法可以比较`pObject`参数和此[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)对象表示的值的地址;如果地址相等，则对象可以视为相等。

## <a name="see-also"></a>请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
