---
title: IDebug内存上下文2：：添加 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Add
helpviewer_keywords:
- IDebugMemoryContext2::Add method
- Add method
ms.assetid: 3c47e646-ce9e-4dd3-8f1a-6dbd3827d407
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a21fa2ec6d48bb1d6bf17bbc0d2ebf0d90a25a9f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727480"
---
# <a name="idebugmemorycontext2add"></a>IDebugMemoryContext2::Add
将指定的值添加到当前上下文并返回新上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT Add( 
   UINT64                 dwCount,
   IDebugMemoryContext2** ppMemCxt
);
```

```csharp
int Add(
   ulong                    dwCount,
   out IDebugMemoryContext2 ppMemCxt
);
```

## <a name="parameters"></a>参数
`dwCount`\
[在]要添加到当前上下文的值。

`ppMemCxt`\
[出]返回新的[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 内存上下文是地址，因此向地址添加值会产生需要新上下文接口的新地址。

 此方法必须始终生成新上下文，即使生成的地址位于与此上下文关联的内存空间之外也是如此。 唯一的例外是，如果无法为新上下文分配内存，或者是否`ppMemCxt`为空值（这是一个错误）。

## <a name="see-also"></a>请参阅
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
