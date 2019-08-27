---
title: IDebugBinder3::GetTypeArguments | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetTypeArguments
helpviewer_keywords:
- IDebugBinder3::GetTypeArguments method
ms.assetid: fa0c37a7-327f-463e-9a9d-bb3f534584cb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a9d301dbb99e88ba4552ad59d9116f64dc032371
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66330745"
---
# <a name="idebugbinder3gettypearguments"></a>IDebugBinder3::GetTypeArguments
此方法检索与此对象关联的参数类型的列表。

## <a name="syntax"></a>语法

```cpp
HRESULT GetTypeArguments(
   UINT          skip,
   UINT          count,
   IDebugField** ppFields,
   UINT*         pFetched
);
```

```csharp
int GetTypeArguments(
   uint          skip,
   uint          count,
   IDebugField[] ppFields,
   out uint      pFetched
);
```

## <a name="parameters"></a>参数
`skip`\
[in]若要获取参数类型之前跳过的字段数。

`count`\
[in]要返回的参数字段数 (还指定的大小`ppFields`数组)。

`ppFields`\
[in、 out]会在此方法返回填充的字段的数组。

`pFetched`\
[out]\(可选)实际返回的字段类型的参数的数量。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 自变量类型的数即可获得事先[GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)。

## <a name="see-also"></a>请参阅
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)