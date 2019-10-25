---
title: IDiaEnumSymbols::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbols::Item method
ms.assetid: 2bd1ec04-e677-4e32-8e32-33334f1eed77
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 12766fe52f7f515b7ca411b17d58117e4e56cc9f
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743951"
---
# <a name="idiaenumsymbolsitem"></a>IDiaEnumSymbols::Item
通过索引检索符号。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   DWORD        index,
   IDiaSymbol** symbol
);
```

#### <a name="parameters"></a>参数
 索引

中要检索的[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象的索引。 索引的范围为0到 `count`-1，其中 `count` 由[IDiaEnumSymbols：： get_Count](../../debugger/debug-interface-access/idiaenumsymbols-get-count.md)方法返回。

 symbol

弄返回一个[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，该对象表示所需的符号。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)