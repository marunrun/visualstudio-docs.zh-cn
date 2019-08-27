---
title: IDiaEnumSymbolsByAddr::symbolByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbolsByAddr::symbolByVA method
ms.assetid: ac84339f-70c6-48ed-85d0-6d7d1b5194e8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a0b97b30b6f19e367cfbae72be29b6d8961f4e1a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833406"
---
# <a name="idiaenumsymbolsbyaddrsymbolbyva"></a>IDiaEnumSymbolsByAddr::symbolByVA
枚举数定位通过按虚拟地址 (VA) 执行查找。

## <a name="syntax"></a>语法

```C++
HRESULT symbolByVA ( 
   DWORD**      virtualAddress,
   IDiaSymbol** ppsymbol
);
```

#### <a name="parameters"></a>参数
 virtualAddress

[in]虚拟地址。

 ppsymbol

[out]返回[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，表示找到的符号。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果找不到符号。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)