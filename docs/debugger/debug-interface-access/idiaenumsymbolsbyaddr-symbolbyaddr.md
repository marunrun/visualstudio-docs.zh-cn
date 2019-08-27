---
title: IDiaEnumSymbolsByAddr::symbolByAddr | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbolsByAddr::symbolByAddr method
ms.assetid: 0b6f5a68-8402-4f29-8219-20576fda8166
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8620dcf7367914e25411fad7ac54a34a5bac54c2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833316"
---
# <a name="idiaenumsymbolsbyaddrsymbolbyaddr"></a>IDiaEnumSymbolsByAddr::symbolByAddr
枚举数定位通过查找按映像部分数量和偏移量。

## <a name="syntax"></a>语法

```C++
HRESULT symbolByAddr ( 
   DWORD**      isect,
   DWORD**      offsect,
   IDiaSymbol** ppsymbol
);
```

#### <a name="parameters"></a>参数
 isect

[in]图像部分数。

 offsect

[in]在部分中的偏移量。

 ppsymbol

[out]返回[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，表示找到的符号。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果找不到符号。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)