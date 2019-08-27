---
title: IDebugReference2::GetDerivedMostReference | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetDerivedMostReference
helpviewer_keywords:
- IDebugReference2::GetDerivedMostReference
ms.assetid: 07253b74-7d39-48e0-8e85-ac8dfd919f6e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8775087b9ec212f7e7d7e1547d01a5f175c4dc22
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329827"
---
# <a name="idebugreference2getderivedmostreference"></a>IDebugReference2::GetDerivedMostReference
获取引用的派生程度最大引用。 留待将来使用。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDerivedMostReference( 
   IDebugReference2** ppDerivedMost
);
```

```csharp
int GetDerivedMostReference( 
   out IDebugReference2 ppDerivedMost
);
```

## <a name="parameters"></a>参数
`ppDerivedMost`\
[out]返回[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)表示派生程度最大属性的对象。

## <a name="return-value"></a>返回值
 始终返回 `E_NOTIMPL`。

## <a name="remarks"></a>备注
 例如，如果此属性描述一个对象，实现`ClassRoot`这是实际的实例化，但`ClassDerived`派生自`ClassRoot`，则此方法返回[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)对象表示对引用`ClassDerived`对象。

## <a name="see-also"></a>请参阅
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)