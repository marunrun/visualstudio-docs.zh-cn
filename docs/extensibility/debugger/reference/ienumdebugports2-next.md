---
title: IEnumDebugPorts2::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2::Next
helpviewer_keywords:
- IEnumDebugPorts2::Next
ms.assetid: 3f43d18c-6bd1-4ddd-95ef-9550abd2ad09
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2245bc6032ebb8df400f595079039b49cee08075
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66339321"
---
# <a name="ienumdebugports2next"></a>IEnumDebugPorts2::Next
枚举中返回下一组元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Next(
   ULONG         celt,
   IDebugPort2** rgelt,
   ULONG*        pceltFetched
);
```

```csharp
int Next(
   uint          celt,
   IDebugPort2[] rgelt,
   ref uint      pceltFetched
);
```

## <a name="parameters"></a>参数
`celt`\
[in]要检索的元素数。 此外可以指定的最大大小`rgelt`数组。

`rgelt`\
[in、 out]数组[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)要填充的元素。

`pceltFetched`\
[out]返回中实际返回的元素数目`rgelt`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果无法返回请求的元素数少于; 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)