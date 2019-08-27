---
title: IDiaEnumTables::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Skip method
ms.assetid: 5c9db956-0654-4f1a-8775-530aa980d8ec
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 24232878452082dd1769c9bc9f1cd22d081968f2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832654"
---
# <a name="idiaenumtablesskip"></a>IDiaEnumTables::Skip
跳过枚举序列中的表的指定的数目。

## <a name="syntax"></a>语法

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>参数
 `celt`

[in]若要跳过枚举序列中的表数。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`如果有多个要跳过的表。

## <a name="see-also"></a>请参阅
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)