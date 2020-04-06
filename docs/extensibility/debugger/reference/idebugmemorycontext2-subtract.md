---
title: IDebug内存上下文2：：减去 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Subtract
helpviewer_keywords:
- Subtract method
- IDebugMemoryContext2::Subtract method
ms.assetid: 63df14c7-8d7e-47c1-afa7-5a1ab5d8eaba
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c858beb8c3f9f587633dbae8b3b1fe73fd789663
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727447"
---
# <a name="idebugmemorycontext2subtract"></a>IDebugMemoryContext2::Subtract
从当前上下文中减去指定值并返回新上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT Subtract( 
   UINT64                 dwCount,
   IDebugMemoryContext2** ppMemCxt
);
```

```csharp
int Subtract(
   ulong                    dwCount,
   out IDebugMemoryContext2 ppMemCxt
);
```

## <a name="parameters"></a>参数
`dwCount`\
[在]要减少的内存字节数。

`ppMemCxt`\
[出]返回新的[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 内存上下文是地址，因此从地址中减去值会产生需要新上下文接口的新地址。

 此方法必须始终生成新上下文，即使生成的地址位于与此上下文关联的内存空间之外也是如此。 唯一的例外是，如果无法为新上下文分配内存，或者是否`ppMemCxt`为空值（这是一个错误）。

## <a name="see-also"></a>请参阅
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
