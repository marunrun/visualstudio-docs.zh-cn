---
title: IEnumDebugThreads2::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugThreads2::Skip
helpviewer_keywords:
- IEnumDebugThreads2::Skip
ms.assetid: eab068d4-1f8d-44cd-bc54-92a10fe23de6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5470c425e9a7f60b1d7f816bfcd4863ee9424b12
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350799"
---
# <a name="ienumdebugthreads2skip"></a>IEnumDebugThreads2::Skip
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
- [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)