---
title: IDebugGenericFieldInstance::TypeArgumentCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- TypeArgumentCount
- IDebugGenericFieldInstance::TypeArgumentCount
ms.assetid: e662c5ea-a5c1-478e-a268-5980dadffcd1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 89f1a92cc5e595bd2574174f0d0776c6605e42da
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66337016"
---
# <a name="idebuggenericfieldinstancetypeargumentcount"></a>IDebugGenericFieldInstance::TypeArgumentCount
返回此实例的参数自变量类型的数目。

## <a name="syntax"></a>语法

```cpp
HRESULT TypeArgumentCount(
   ULONG32* pcArgs
);
```

```csharp
int TypeArgumentCount(
   ref uint pcArgs
);
```

## <a name="parameters"></a>参数
`pcArgs`\
[in、 out]此实例的类型参数参数的数目。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 例如，如果列表\<int >，此方法返回 1，并且，如果列表\<int，float2 > 此方法返回 2。 如果没有任何类型自变量，则此方法返回 0。

## <a name="see-also"></a>请参阅
- [IDebugGenericFieldInstance](../../../extensibility/debugger/reference/idebuggenericfieldinstance.md)