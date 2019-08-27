---
title: IDiaEnumSymbolsByAddr::Prev | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbolsByAddr::Prev method
ms.assetid: da3b3dca-68cb-4cb0-b25c-e28a1ffe49d3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4a1b69dbd7e502340e7d563523288a095b733c2d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62830254"
---
# <a name="idiaenumsymbolsbyaddrprev"></a>IDiaEnumSymbolsByAddr::Prev
按地址检索顺序中的上一个符号。

## <a name="syntax"></a>语法

```C++
HRESULT Prev ( 
   ULONG        celt,
   IDiaSymbol** rgelt,
   ULONG*       pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

[in]要检索的枚举器中的符号数。

 rgelt

[out]数组，它是在用来填充[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象表示所需的符号。

 pceltFetched

[out]在提取枚举器返回的符号的数量。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果没有上一个符号。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法更新枚举器位置提取的元素数。

## <a name="see-also"></a>请参阅
- [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)