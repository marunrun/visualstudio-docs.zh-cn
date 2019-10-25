---
title: IDiaSymbol::get_numberOfRows | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: cf3eb110-d07f-4995-b68b-08290aa67d6f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 257a667d8c2347394abaaa3282b37201d443ed97
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739649"
---
# <a name="idiasymbolget_numberofrows"></a>IDiaSymbol::get_numberOfRows
检索矩阵中的行数。

## <a name="syntax"></a>语法

```C++
HRESULT get_numberOfRows(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄一个指针，指向包含矩阵中的行数的 `DWORD`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)