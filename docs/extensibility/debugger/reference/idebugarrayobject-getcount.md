---
title: IDebugArrayObject：： GetCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetCount
helpviewer_keywords:
- IDebugArrayObject::GetCount method
ms.assetid: 7931f3f7-033c-4bf8-8abd-95183952ebb0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d9d5e322b7bcd5238335c74caa21989f1f1962ce
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80736209"
---
# <a name="idebugarrayobjectgetcount"></a>IDebugArrayObject::GetCount
获取数组中元素的计数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCount( 
   DWORD* pdwElements
);
```

```csharp
int GetCount(
   out uint pdwElements
);
```

## <a name="parameters"></a>参数
`pdwElements`\
弄返回计数。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 此方法将数组对象的所有元素视为一维数组，即使数组对象是多维的。 例如，给定数组 `myarray[3][2][6]` ，此方法将在参数中返回 36 `pdwElements` 。 使用 [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md) 方法每次检索一个元素。

## <a name="see-also"></a>另请参阅
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
