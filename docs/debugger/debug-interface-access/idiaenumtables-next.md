---
title: IDiaEnumTables::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Next method
ms.assetid: 8d7bd359-d33e-4317-9674-d89283efd7de
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 688652fe3915e1974d5d0e1d04fb1ac075863d8c
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743745"
---
# <a name="idiaenumtablesnext"></a>IDiaEnumTables::Next
检索枚举序列中指定数量的表。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
   ULONG       celt,
   IDiaTable** rgelt,
   ULONG*      pceltFetched
);
```

#### <a name="parameters"></a>参数
 `celt`

中要检索的枚举器中的表数。

 `rgelt`

弄要使用表示所需表的[IDiaTable](../../debugger/debug-interface-access/idiatable.md)对象填充的数组。

 `pceltFetched`

弄返回提取的枚举器中的表数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多表，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)