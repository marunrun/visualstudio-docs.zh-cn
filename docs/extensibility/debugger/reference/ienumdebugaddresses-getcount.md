---
title: IEnumDebugAddresses::GetCount | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses::GetCount
helpviewer_keywords:
- IEnumDebugAddresses::GetCount method
ms.assetid: f2ca8ff8-539f-457c-83f8-9bbf97618065
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a718679441f93131bc545aa3062f2b9a68893f9e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66347304"
---
# <a name="ienumdebugaddressesgetcount"></a>IEnumDebugAddresses::GetCount
此方法返回的枚举中的元素数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCount(
   [out] ULONG* pcelt
);
```

```csharp
int GetCount(
   out uint pcelt
);
```

## <a name="parameters"></a>参数
`pcelt`\
[out]枚举中返回元素的数。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 此方法不是惯用的 COM 枚举接口指定的下一步、 克隆、 跳过和重置需要实现的一部分。

## <a name="see-also"></a>请参阅
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)