---
title: IDiaEnumSymbolsByAddr::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbolsByAddr::Next method
ms.assetid: a1320587-7ce7-401f-9548-2f8bcece5cc3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e52567eddcbb6c4f372256e66b7b723bc7aa7394
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833436"
---
# <a name="idiaenumsymbolsbyaddrnext"></a>IDiaEnumSymbolsByAddr::Next
检索地址按顺序的下一个符号。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
   ULONG        celt,
   IDiaSymbol** rgelt,
   ULONG*       pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

[in]要检索的枚举器中的符号数。

 rgelt

[out]数组，它是在用来填充[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，表示所需的符号。

 pceltFetched

[out]在提取枚举器返回的符号的数量。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果没有更多的符号。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法更新枚举器位置提取的元素数。

## <a name="see-also"></a>请参阅
- [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)