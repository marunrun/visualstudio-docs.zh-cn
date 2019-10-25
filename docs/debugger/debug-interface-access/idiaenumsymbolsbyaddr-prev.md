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
ms.openlocfilehash: 70265976e5c6e7c2b3f536f2b8648aaba44df528
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743862"
---
# <a name="idiaenumsymbolsbyaddrprev"></a>IDiaEnumSymbolsByAddr::Prev
按地址检索前面的符号。

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

中要检索的枚举器中的符号数。

 rgelt

弄要用[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象填充的数组，这些对象表示所需的符号。

 pceltFetched

弄返回提取的枚举器中的符号数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有以前的符号，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法按提取的元素数更新枚举器的位置。

## <a name="see-also"></a>请参阅
- [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)