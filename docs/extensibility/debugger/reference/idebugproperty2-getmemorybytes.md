---
title: IDebug属性2：：获取内存字节 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetMemoryBytes
helpviewer_keywords:
- IDebugProperty2::GetMemoryBytes
ms.assetid: b32042ed-7a06-4b4a-99ef-fe03b0aa61cc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7d13fa3821a6d7bf861cd160a5588d0788b92243
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721476"
---
# <a name="idebugproperty2getmemorybytes"></a>IDebugProperty2::GetMemoryBytes
获取构成属性值的内存字节。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMemoryBytes ( 
   IDebugMemoryBytes2** ppMemoryBytes
);
```

```csharp
int GetMemoryBytes ( 
   out IDebugMemoryBytes2 ppMemoryBytes
);
```

## <a name="parameters"></a>参数
`ppMemoryBytes`\
[出]返回可用于检索包含属性值的内存的[IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则返回错误代码。 如果没有`S_GETMEMORYBYTES_NO_MEMORY_BYTES`要检索的内存字节，则返回。

## <a name="see-also"></a>请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
