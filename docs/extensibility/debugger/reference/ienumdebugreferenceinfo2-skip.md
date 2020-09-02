---
title: IEnumDebugReferenceInfo2：： Skip |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugReferenceInfo2::Skip
helpviewer_keywords:
- IEnumDebugReferenceInfo2::Skip
ms.assetid: 12f07ed8-92bd-47b5-9113-f73fec5bdde6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2c2247b30d1f300992ef86f80fe44e8ea680fc15
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80715286"
---
# <a name="ienumdebugreferenceinfo2skip"></a>IEnumDebugReferenceInfo2::Skip
跳过指定数目的元素。

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
中要跳过的元素数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 `S_FALSE`如果 `celt` 大于剩余元素的数目，则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 如果 `celt` 指定的值大于剩余元素的数目，则枚举将设置为 end，并 `S_FALSE` 返回。

## <a name="see-also"></a>另请参阅
- [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)
