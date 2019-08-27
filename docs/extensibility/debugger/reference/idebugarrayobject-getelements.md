---
title: IDebugArrayObject::GetElements |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetElements
helpviewer_keywords:
- IDebugArrayObject::GetElements method
ms.assetid: f6a6262f-5183-46ce-8a45-33ef46088b98
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 915724fa5790c6b8c9fde2706b1222db239cb4ab
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351800"
---
# <a name="idebugarrayobjectgetelements"></a>IDebugArrayObject::GetElements
获取数组的所有元素的枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT GetElements( 
   IEnumDebugObjects** ppEnum
);
```

```csharp
int GetElements(
   out IEnumDebugObjects ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
[out]返回[IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)对象，它允许枚举的所有元素。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 或者，使用[GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md)并[GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)方法来循环访问元素。

## <a name="see-also"></a>请参阅
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)