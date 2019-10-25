---
title: IDiaSymbol::get_thunkOrdinal | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_thunkOrdinal method
ms.assetid: 4b28d78a-1974-4d8a-8bb7-781bf630f2f4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3bc8c523886d694ea413dedcf9a28e53e361882b
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739140"
---
# <a name="idiasymbolget_thunkordinal"></a>IDiaSymbol::get_thunkOrdinal
检索函数的 thunk 类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_thunkOrdinal ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回[THUNK_ORDINAL 枚举](../../debugger/debug-interface-access/thunk-ordinal.md)枚举中的一个值，该值指定函数的 THUNK 类型。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 仅当符号为 `SymTagThunk` 的[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值时，此属性才有效。

 "Thunk" 是一段代码，用于在32位内存地址空间（也称为平面地址空间）和16位地址空间（称为分段地址空间）之间进行转换。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [THUNK_ORDINAL 枚举](../../debugger/debug-interface-access/thunk-ordinal.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)