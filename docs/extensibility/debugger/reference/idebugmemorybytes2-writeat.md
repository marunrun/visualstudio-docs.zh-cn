---
title: IDebug记忆字节2：：写 at |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2::WriteAt
helpviewer_keywords:
- IDebugMemoryBytes2::WriteAt method
- WriteAt method
ms.assetid: 61cc3704-47fa-4d9b-aa62-bb4585ac8fb1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ac9113424c6cd5cce230774a6e5335ffa4d4ba77
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727528"
---
# <a name="idebugmemorybytes2writeat"></a>IDebugMemoryBytes2::WriteAt
从指定的地址开始，写入指定的内存字节数。

## <a name="syntax"></a>语法

```cpp
HRESULT WriteAt( 
   IDebugMemoryContext2* pStartContext,
   DWORD                 dwCount,
   BYTE*                 rgbMemory
);
```

```csharp
int WriteAt(
   IDebugMemoryContext2 pStartContext,
   uint                 dwCount,
   byte[]               rgbMemory
);
```

## <a name="parameters"></a>参数
`pStartContext`\
[在][IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)对象，指定从何处开始写入字节。

`dwCount`\
[在]要写入的字节数。

`rgbMemory`\
[在]要写入的字节。 此数组假定为大小中至少`dwCount`字节。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，如果`S_FALSE`并非所有字节都可以写入或返回错误代码（通常`E_FAIL`），则返回。

## <a name="remarks"></a>备注
 如果起始地址不在此[IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)对象表示的内存窗口中，则不进行写入并返回 其`E_FAIL`错误代码 -即使写入量重叠到内存空间。

## <a name="see-also"></a>请参阅
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
