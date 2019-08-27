---
title: IEnumDebugBoundBreakpoints2::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugBoundBreakpoints2::Skip
helpviewer_keywords:
- IEnumDebugBoundBreakpoints2::Skip
ms.assetid: 95659709-6d7c-44ca-b598-629eb688429f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ce9c27cfe99679f8e435923eeef49fbadb2b36c5
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66336961"
---
# <a name="ienumdebugboundbreakpoints2skip"></a>IEnumDebugBoundBreakpoints2::Skip
跳过指定数量的元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Skip(
   ULONG celt
);
```

```csharp
int Skip(
   uint celt
);
```

## <a name="parameters"></a>参数
`celt`\
[in]要跳过的元素数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果`celt`大于剩余的元素数; 否则，返回错误代码。

## <a name="remarks"></a>备注
 如果`celt`指定的值数比大剩余元素的枚举设置为结束和`S_FALSE`返回。

## <a name="see-also"></a>请参阅
- [IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)