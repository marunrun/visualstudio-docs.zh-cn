---
title: IEnumDebugFrameInfo2：：跳过 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFrameInfo2::Skip
helpviewer_keywords:
- IEnumDebugFrameInfo2::Skip
ms.assetid: 68cd3948-022a-41ad-bd9f-9ab776cf6248
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f662f810e3bb7bfd746b507dada0f22ff1741854
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716625"
---
# <a name="ienumdebugframeinfo2skip"></a>IEnumDebugFrameInfo2::Skip
跳过指定数量的元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Skip(
   ULONG celt
);
```

```csharp
int Skip(
   uint celt
);
```

## <a name="parameters"></a>参数
`celt`\
[在]要跳过的元素数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果`S_FALSE``celt`大于剩余元素数，则返回;否则，返回错误代码。

## <a name="remarks"></a>备注
 如果`celt`指定大于剩余元素数的值，则枚举将设置为末尾并`S_FALSE`返回。

## <a name="see-also"></a>请参阅
- [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
