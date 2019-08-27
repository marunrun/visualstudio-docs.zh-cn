---
title: 'Idiasymbol:: Get_isstripped |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isStripped method
ms.assetid: cc2c4a0b-ab9f-4b79-a8ff-a3badb0405d6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c46319714e24a64ad71951b78c55c140028c3ab0
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64819094"
---
# <a name="idiasymbolgetisstripped"></a>IDiaSymbol::get_isStripped
检索标志，指示是否从符号文件中已去除私有符号。

## <a name="syntax"></a>语法

```C++
HRESULT get_isStripped(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out]返回`TRUE`私有符号已从符号文件中; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="remarks"></a>备注
 此属性是可从`SymTagExe`符号类型 (请参阅[Exe](../../debugger/debug-interface-access/exe.md))。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Exe](../../debugger/debug-interface-access/exe.md)