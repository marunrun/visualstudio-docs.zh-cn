---
title: IDiaSymbol::get_registerId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_registerId method
ms.assetid: f881e793-eb9e-48dc-a847-dd61d77174fc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6ffd349b56c4292de04d5d7a38e82eeafed6775e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739466"
---
# <a name="idiasymbolget_registerid"></a>IDiaSymbol::get_registerId
当[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)设置为 `LocIsEnregistered` 时，检索位置的注册指示符。

## <a name="syntax"></a>语法

```C++
HRESULT get_registerId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回位置的注册指示符。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 如果符号是相对于寄存器的，即，如果符号的[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)设置为 `LocIsRegRel`，请使用 `get_registerId` 方法，然后调用[IDiaSymbol：： get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md)方法，以获取来自寄存器（其中符号为）的偏移量。遍布.

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)