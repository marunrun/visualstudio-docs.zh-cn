---
title: IDebugPendingBreakpoint2::SetCondition | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::SetCondition
helpviewer_keywords:
- SetCondition method
- IDebugPendingBreakpoint2::SetCondition method
ms.assetid: 0534224f-654f-4862-bc4d-a9a81a5f8899
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1a71e22d118b64e15bb9da15b2f9152a90440f1a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66347654"
---
# <a name="idebugpendingbreakpoint2setcondition"></a>IDebugPendingBreakpoint2::SetCondition
设置或更改关联挂起断点的条件。

## <a name="syntax"></a>语法

```cpp
HRESULT SetCondition( 
   BP_CONDITION bpCondition
);
```

```csharp
int SetCondition( 
   BP_CONDITION bpCondition
);
```

## <a name="parameters"></a>参数
`bpCondition`\
[in]一个[BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)结构，它指定要设置的条件。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 以前挂起断点有关联任何条件会丢失。 从该绑定挂起断点的所有断点都调用以将其条件设置中指定的值为`bpCondition`参数。

## <a name="see-also"></a>请参阅
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)