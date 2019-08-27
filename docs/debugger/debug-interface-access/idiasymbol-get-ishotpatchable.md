---
title: 'Idiasymbol:: Get_ishotpatchable |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isHotpatchable method
ms.assetid: b7b6f490-1cf2-4a68-9237-b152dac84d3c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6ac1547228be6312126bb48602e3a77fed0b3c25
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64811200"
---
# <a name="idiasymbolgetishotpatchable"></a>IDiaSymbol::get_isHotpatchable
检索一个标志，指示是否编译该模块[/hotpatch （创建可热修补映像）](/cpp/build/reference/hotpatch-create-hotpatchable-image)编译器开关。

## <a name="syntax"></a>语法

```C++
HRESULT get_isHotpatchable(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out]返回`TRUE`如果该模块可热修补; 否则为返回`FALSE`。

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