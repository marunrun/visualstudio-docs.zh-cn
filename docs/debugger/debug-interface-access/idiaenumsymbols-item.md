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
ms.openlocfilehash: 91c230f641612c099495c54db67da9c7e755cbdc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829440"
---
# <a name="idiaenumsymbolsitem"></a>IDiaEnumSymbols::Item
通过索引中检索一个符号。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   DWORD        index,
   IDiaSymbol** symbol
);
```

#### <a name="parameters"></a>参数
 索引

[in]索引[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)要检索对象。 索引是 0 到范围内`count`-1，其中`count`返回的[idiaenumsymbols:: Get_count](../../debugger/debug-interface-access/idiaenumsymbols-get-count.md)方法。

 symbol

[out]返回[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，表示所需的符号。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)