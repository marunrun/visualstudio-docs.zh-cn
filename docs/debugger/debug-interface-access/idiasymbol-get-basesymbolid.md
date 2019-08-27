---
title: IDiaSymbol::get_baseSymbolId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: cd504d2b-194f-4106-8de5-2de827a79cbd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8880d207a41418e12cab4374578fea4f3c4f338c
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62837710"
---
# <a name="idiasymbolgetbasesymbolid"></a>IDiaSymbol::get_baseSymbolId
检索从其基于指针的符号 ID。

## <a name="syntax"></a>语法

```C++
HRESULT get_baseSymbolId(
   DWORD *pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]一个指向`DWORD`用于保存从其基于指针的符号 ID。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_baseSymbol](../../debugger/debug-interface-access/idiasymbol-get-basesymbol.md)