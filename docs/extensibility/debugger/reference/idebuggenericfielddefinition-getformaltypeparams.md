---
title: IDebugGenericFieldDefinition::GetFormalTypeParams | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetFormalTypeParams
- IDebugGenericFieldDefinition::GetFormalTypeParams
ms.assetid: cadbd6a1-bc7c-4aff-8777-5396b7a23c3e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 164bb5c3f74dec9a56ce3146c5e7ec62d6eb46b4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66313168"
---
# <a name="idebuggenericfielddefinitiongetformaltypeparams"></a>IDebugGenericFieldDefinition::GetFormalTypeParams
检索给定的参数数目的类型参数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetFormalTypeParams(
   ULONG32                   cParams,
   IDebugGenericParamField** ppParams,
   ULONG32*                  pcParams
);
```

```csharp
int GetFormalTypeParams(
   uint                          cParams,
   out IDebugGenericParamField[] ppParams,
   ref uint                      pcParams
);
```

## <a name="parameters"></a>参数
`cParams`\
[in]参数数目。

`ppParams`\
[out]类型参数的数组。

`pcParams`\
[in、 out]中的参数数量`ppParams`数组。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 返回的类型参数的顺序从左到右。 例如，字典\<K，V > 将返回 IDebugFormalGenericParameters {K，V}。

## <a name="see-also"></a>请参阅
- [IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)