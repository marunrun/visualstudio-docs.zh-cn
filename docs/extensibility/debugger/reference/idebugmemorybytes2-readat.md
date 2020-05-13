---
title: IDebug记忆字节2：：阅读AT |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2::ReadAt
helpviewer_keywords:
- IDebugMemoryBytes2::ReadAt method
- ReadAt method
ms.assetid: b413684d-4155-4bd4-ae30-ffa512243b5f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f909ac3d2e2993879e4c24140abbf23c2ee8d545
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727531"
---
# <a name="idebugmemorybytes2readat"></a>IDebugMemoryBytes2::ReadAt
从给定位置开始读取字节序列。

## <a name="syntax"></a>语法

```cpp
HRESULT ReadAt( 
   IDebugMemoryContext2* pStartContext,
   DWORD                 dwCount,
   BYTE*                 rgbMemory,
   DWORD*                pdwRead,
   DWORD*                pdwUnreadable
);
```

```csharp
int ReadAt(
   IDebugMemoryContext2 pStartContext,
   uint                 dwCount,
   byte[]               rgbMemory,
   out uint             pdwRead,
   ref uint             pdwUnreadable
);
```

## <a name="parameters"></a>参数
`pStartContext`\
[在][IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)对象，指定从何处开始读取字节。

`dwCount`\
[在]要读取的字节数。 还指定数组的长度`rgbMemory`。

`rgbMemory`\
[进出]填充的字节数组实际读取。

`pdwRead`\
[出]返回实际读取的连续字节数。

`pdwUnreadable`\
[进出]返回不可读字节的数量。 如果客户端对不可读字节数不感兴趣，则可能是 null 值。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 如果请求 100 个字节，并且前 50 个字节可读，则接下来的 20 个不可读，其余 30 个字节是可读的，则此方法将返回：

 *`pdwRead`= 50

 *`pdwUnreadable`= 20

 在这种情况下，由于`*pdwRead + *pdwUnreadable < dwCount`调用方必须进行额外的调用才能读取原始 100 个请求的剩余 30 个字节，`pStartContext`并且参数中传递的[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)对象必须提前 70 个。

## <a name="see-also"></a>请参阅
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
