---
title: IDebugProperty2::GetMemoryContext | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetMemoryContext
helpviewer_keywords:
- IDebugProperty2::GetMemoryContext
ms.assetid: 91793d25-790f-4881-a5c0-d0458e534514
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 84ea336050582e2f23aafbbf74599f92c82d20fc
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66343075"
---
# <a name="idebugproperty2getmemorycontext"></a>IDebugProperty2::GetMemoryContext
获取属性值的内存上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMemoryContext ( 
   IDebugMemoryContext2** ppMemory
);
```

```csharp
int GetMemoryContext(
   out IDebugMemoryContext2 ppMemory
);
```

## <a name="parameters"></a>参数
`ppMemory`\
[out]返回[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)对象，表示与此属性关联的内存。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则返回错误代码。 返回`S_GETMEMORYCONTEXT_NO_MEMORY_CONTEXT`如果没有内存上下文来检索。

## <a name="see-also"></a>请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)