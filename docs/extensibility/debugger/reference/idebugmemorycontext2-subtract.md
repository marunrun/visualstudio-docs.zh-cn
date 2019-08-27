---
title: IDebugMemoryContext2::Subtract | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Subtract
helpviewer_keywords:
- Subtract method
- IDebugMemoryContext2::Subtract method
ms.assetid: 63df14c7-8d7e-47c1-afa7-5a1ab5d8eaba
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a320b7c67cd2603dfea11983d2d62c344f347ab4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66347023"
---
# <a name="idebugmemorycontext2subtract"></a>IDebugMemoryContext2::Subtract
从当前上下文中的指定的值减去，并返回新的上下文。

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
[in]要递减的内存字节数。

`ppMemCxt`\
[out]返回一个新[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 内存上下文是一个地址，因此从发件人地址值中减去生成需要新的上下文接口的新地址。

 即使生成的地址是与此上下文关联的内存空间外，此方法必须始终会生成一个新的上下文。 唯一的例外是，如果可以为新的上下文不分配任何内存或`ppMemCxt`为空值 （这是错误）。

## <a name="see-also"></a>请参阅
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)