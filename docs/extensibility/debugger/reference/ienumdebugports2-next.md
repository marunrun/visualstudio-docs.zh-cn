---
title: IEnumDebugPorts2：：下一个 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2::Next
helpviewer_keywords:
- IEnumDebugPorts2::Next
ms.assetid: 3f43d18c-6bd1-4ddd-95ef-9550abd2ad09
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 66cb525157d5902b43a9924291d7c10260b40309
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716164"
---
# <a name="ienumdebugports2next"></a>IEnumDebugPorts2::Next
从枚举返回下一组元素。

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
[在]要检索的元素数。 还指定`rgelt`数组的最大大小。

`rgelt`\
[进出]要填充的[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)元素的数组。

`pceltFetched`\
[出]返回 中`rgelt`实际返回的元素数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果`S_FALSE`返回的元素数少于请求的元素数，则返回;否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
