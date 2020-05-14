---
title: IDebug内存上下文2：：比较 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Compare
helpviewer_keywords:
- IDebugMemoryContext2::Compare method
- Compare method
ms.assetid: c51b5128-848e-4d8e-b2e9-1161339763c3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4b2551f8554d96186b90a1eed97a5a48ec5f0405
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727491"
---
# <a name="idebugmemorycontext2compare"></a>IDebugMemoryContext2::Compare
以比较标志指示的方式将内存上下文与给定数组中的每个上下文进行比较，返回匹配的第一个上下文的索引。

## <a name="syntax"></a>语法

```cpp
HRESULT Compare( 
   CONTEXT_COMPARE        compare,
   IDebugMemoryContext2** rgpMemoryContextSet,
   DWORD                  dwMemoryContextSetLen,
   DWORD*                 pdwMemoryContext
);
```

```csharp
int Compare(
   enum_CONTEXT_COMPARE   compare,
   IDebugMemoryContext2[] rgpMemoryContextSet,
   uint                   dwMemoryContextSetLen,
   out uint               pdwMemoryContext
);
```

## <a name="parameters"></a>参数
`compare`\
[在][CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md)枚举中确定比较类型的值。

`rgpMemoryContextSet`\
[在]要与之比较的[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)对象的引用数组。

`dwMemoryContextSetLen`\
[在]数组中的`rgpMemoryContextSet`上下文数。

`pdwMemoryContext`\
[出]返回满足比较的第一个内存上下文的索引。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。 如果`E_COMPARE_CANNOT_COMPARE`无法比较这两个上下文，则返回。

## <a name="remarks"></a>备注
 调试引擎 （DE） 不必支持所有类型的比较，`CONTEXT_EQUAL`但它必须至少支持 和`CONTEXT_LESS_THAN`。 `CONTEXT_GREATER_THAN` `CONTEXT_SAME_SCOPE`

## <a name="see-also"></a>请参阅
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
- [CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md)
