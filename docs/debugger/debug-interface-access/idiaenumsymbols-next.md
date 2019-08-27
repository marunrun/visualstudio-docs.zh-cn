---
title: 'Idiaenumsymbols:: Next |Microsoft Docs'
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
ms.openlocfilehash: ef151b369c18863b8a87944cdbf69fed9aeb0840
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833384"
---
# <a name="idiaenumsymbolsnext"></a>IDiaEnumSymbols::Next
检索指定的数目的枚举序列中的符号。

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

[out]数组，它是在用来填充[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象表示所需的符号。

 pceltFetched

[out]在提取枚举器返回的符号的数量。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果没有更多的符号。 否则，返回错误代码。

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