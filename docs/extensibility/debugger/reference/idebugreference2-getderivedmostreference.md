---
title: IDebug 参考2：：获取最参考 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetDerivedMostReference
helpviewer_keywords:
- IDebugReference2::GetDerivedMostReference
ms.assetid: 07253b74-7d39-48e0-8e85-ac8dfd919f6e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 15e98884d040cfb2ebf1b33a56c7edea331fbff0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720613"
---
# <a name="idebugreference2getderivedmostreference"></a>IDebugReference2::GetDerivedMostReference
获取引用的派生最大引用。 保留供将来使用。

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
[出]返回表示派生最派生属性的[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)对象。

## <a name="return-value"></a>返回值
 始终返回 `E_NOTIMPL`。

## <a name="remarks"></a>备注
 例如，如果`ClassRoot`此属性描述实现但实际上是派生自`ClassDerived``ClassRoot`的对象的对象，则此方法返回表示对对象的引用的`ClassDerived` [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)对象。

## <a name="see-also"></a>请参阅
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
