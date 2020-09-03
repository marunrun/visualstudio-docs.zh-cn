---
title: IDebugObject：： IsEqual |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
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
中表示要比较的对象的 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象。

`pfIsEqual`\
弄如果对象的值相等，则返回非零 (`TRUE`) ; 否则返回零 (`FALSE`) 。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 通常，此方法可以比较 `pObject` 参数和此 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象所表示的值的地址; 如果地址相等，则可以将这些对象视为相等。

## <a name="see-also"></a>另请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
