---
title: IDiaSymbol：： get_baseSymbol |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: cabb5a18-bda7-47e8-9e46-5f4718579fc9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 307358522609659a8a95b94a0adf037026f5b948
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740940"
---
# <a name="idiasymbolget_basesymbol"></a>IDiaSymbol::get_baseSymbol
检索指针所基于的符号。

## <a name="syntax"></a>语法

```C++
HRESULT get_baseSymbol(
   IDiaSymbol** pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄指向指针所基于的符号的指针。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_baseSymbolId](../../debugger/debug-interface-access/idiasymbol-get-basesymbolid.md)