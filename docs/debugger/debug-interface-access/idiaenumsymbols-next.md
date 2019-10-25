---
title: IDiaEnumSymbols：： Next |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbols::Next method
ms.assetid: bfe5fe27-6a84-4392-910f-e325146d7552
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c2d754c144ad876890b89ea217bf0ac55ad60b24
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743934"
---
# <a name="idiaenumsymbolsnext"></a>IDiaEnumSymbols::Next
检索枚举序列中指定数目的符号。

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

中要检索的枚举器中的符号数。

 rgelt

弄要使用表示所需符号的[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象填充的数组。

 pceltFetched

弄返回提取的枚举器中的符号数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多符号，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="example"></a>示例

```C++
IDiaEnumSymbols* pEnum
CComPtr< IDiaSymbol> pSym;
DWORD celt;
pEnum->Next( 1, &pSym, &celt );
```

## <a name="see-also"></a>请参阅
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)