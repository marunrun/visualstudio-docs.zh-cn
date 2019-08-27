---
title: IDiaSymbol::get_isMSILNetmodule | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isMSILNetmodule method
ms.assetid: 593827f3-8437-4a12-ada4-ff715ec95fb2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0cb96291f7a867bcdd0248cc68c2fbccb6ac9f87
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64828801"
---
# <a name="idiasymbolgetismsilnetmodule"></a>IDiaSymbol::get_isMSILNetmodule
检索一个标志，指示模块是否一个.netmodule （只包含元数据，并且没有本机符号是 Microsoft 中间语言 (MSIL) 模块）。

## <a name="syntax"></a>语法

```C++
HRESULT get_isMSILNetmodule(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out]返回`TRUE`如果模块是 MSIL; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="remarks"></a>备注
 此属性是可从`SymTagCompilandDetails`符号类型 (请参阅[CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md))。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)