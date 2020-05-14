---
title: IEnum调试程序2：：下一个 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPrograms2::Next
helpviewer_keywords:
- IEnumDebugPrograms2::Next
ms.assetid: 9120e263-e97c-4a40-ab2c-e9264ce3d6c4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 035af638b9504318a39e01f34ed32719d957896e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715623"
---
# <a name="ienumdebugprograms2next"></a>IEnumDebugPrograms2::Next
从枚举返回下一组元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Next(
   ULONG            celt,
   IDebugProgram2** rgelt,
   ULONG*           pceltFetched
);
```

```csharp
int Next(
   uint             celt,
   IDebugProgram2[] rgelt,
   ref uint         pceltFetched
);
```

## <a name="parameters"></a>参数
`celt`\
[在]要检索的元素数。 还指定`rgelt`数组的最大大小。

`rgelt`\
[进出]要填充的[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)元素的数组。

`pceltFetched`\
[出]返回 中`rgelt`实际返回的元素数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果`S_FALSE`返回的元素数少于请求的元素数，则返回;否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
