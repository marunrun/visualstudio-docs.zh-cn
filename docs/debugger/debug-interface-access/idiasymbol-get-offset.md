---
title: IDiaSymbol：： get_offset |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_offset method
ms.assetid: 8292bb08-4dc8-4663-beb4-258f5d5a448d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: feb7620e507c5e57cf025211e42d541440af22f3
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739580"
---
# <a name="idiasymbolget_offset"></a>IDiaSymbol::get_offset
检索符号位置的偏移量。 当[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)`LocIsRegRel` 或 `LocIsBitField` 时使用。

## <a name="syntax"></a>语法

```C++
HRESULT get_offset ( 
   LONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回符号位置的偏移量（以字节为单位）。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 该偏移量来自之前确定的一些已知点。 例如，`LocIsBitField` 位置类型的偏移量通常来自包含类的开头。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)