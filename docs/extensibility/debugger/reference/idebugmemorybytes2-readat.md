---
title: IDebugMemoryBytes2：： ReadAt |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80727531"
---
# <a name="idebugmemorybytes2readat"></a>IDebugMemoryBytes2::ReadAt
读取从给定位置开始的字节序列。

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
中 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 对象，指定开始读取字节的位置。

`dwCount`\
中要读取的字节数。 还指定数组的长度 `rgbMemory` 。

`rgbMemory`\
[in，out]用实际读取的字节填充的数组。

`pdwRead`\
弄返回实际读取的连续字节数。

`pdwUnreadable`\
[in，out]返回不可读字节数。 如果客户端 uninterested 不可读字节数，则可能为 null 值。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 如果请求了100字节，并且第一个50是可读的，则下一个20是不可读的，其余30个为可读，此方法返回：

 *`pdwRead` = 50

 *`pdwUnreadable` = 20

 在这种情况下，由于 `*pdwRead + *pdwUnreadable < dwCount` ，调用方必须执行额外的调用以读取请求的原始100的剩余30个字节，并且参数中传递的 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 对象 `pStartContext` 必须由70提前。

## <a name="see-also"></a>另请参阅
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
