---
title: IDiaSymbol::get_isMatrixRowMajor |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 36b1e881-ea76-48b0-b67f-e9eb0d19bec7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 146ef53f8a5d893e394834c7d5702c8992fdd20a
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62836404"
---
# <a name="idiasymbolgetismatrixrowmajor"></a>IDiaSymbol::get_isMatrixRowMajor
指定矩阵是否为主要的行。

## <a name="syntax"></a>语法

```C++
HRESULT get_isMatrixRowMajor(
   BOOL* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]一个指向`BOOL`指定矩阵是否为主要的行。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)