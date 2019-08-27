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
ms.openlocfilehash: 15a9ebbd3a3993568e4b6496e04661a63290399e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832722"
---
# <a name="idiaenumtablesnext"></a>IDiaEnumTables::Next
检索指定的数目的枚举序列中的表。

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

[in]要检索的枚举器中的表数。

 `rgelt`

[out]数组，它是在用来填充[IDiaTable](../../debugger/debug-interface-access/idiatable.md)表示所需的表的对象。

 `pceltFetched`

[out]在提取枚举器返回的表的数量。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果没有更多的表。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)