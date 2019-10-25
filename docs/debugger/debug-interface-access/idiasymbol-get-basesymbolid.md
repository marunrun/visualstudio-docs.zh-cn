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
ms.openlocfilehash: 3248721afd14ce46745e1eab40a3c4b4f9fbe76a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740925"
---
# <a name="idiasymbolget_basesymbolid"></a>IDiaSymbol::get_baseSymbolId
检索指针所基于的符号 ID。

## <a name="syntax"></a>语法

```C++
HRESULT get_baseSymbolId(
   DWORD *pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄指向 `DWORD` 的指针，该指针包含指针所基于的符号 ID。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_baseSymbol](../../debugger/debug-interface-access/idiasymbol-get-basesymbol.md)