---
title: IDiaEnumSymbolsByAddr::symbolByRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbolsByAddr::symbolByRVA method
ms.assetid: f7828029-f2ee-4ccd-afac-785adc60a4c8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 38d7b0cb8564743ab35cac20cdcb352cdbca48d3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62830267"
---
# <a name="idiaenumsymbolsbyaddrsymbolbyrva"></a>IDiaEnumSymbolsByAddr::symbolByRVA
枚举数定位通过按相对虚拟地址 (RVA) 执行查找。

## <a name="syntax"></a>语法

```C++
HRESULT symbolByRVA ( 
   DWORD**      relativeVirtualAddress,
   IDiaSymbol** ppsymbol
);
```

#### <a name="parameters"></a>参数
 relativeVirtualAddress

[in]地址相对于映像的启动。

 ppsymbol

[out]返回[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，表示找到的符号。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果找不到符号。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)
- [IDiaEnumSymbolsByAddr::symbolByVA](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-symbolbyva.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)