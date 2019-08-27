---
title: 'Idiasymbol:: Get_offset |Microsoft Docs'
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
ms.openlocfilehash: 0016ca267b3eaf2535896aab1ee58a470a192c9a
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64786704"
---
# <a name="idiasymbolgetoffset"></a>IDiaSymbol::get_offset
检索符号位置的偏移的量。 何时使用[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)是`LocIsRegRel`或`LocIsBitField`。

## <a name="syntax"></a>语法

```C++
HRESULT get_offset ( 
   LONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回以字节为单位的符号位置的偏移量。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="remarks"></a>备注
 偏移量是从先前确定的一些已知点。 例如，对于偏移量`LocIsBitField`位置类型通常是从包含类的开头。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)