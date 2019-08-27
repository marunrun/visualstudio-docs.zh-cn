---
title: 'Idiasymbol:: Get_noinline |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_noInline method
ms.assetid: 5c610b78-f1a3-494a-acf8-c42b97935be1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1d0523618298cb6575a5bdb8b92bdc6a4b8c103c
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64786260"
---
# <a name="idiasymbolgetnoinline"></a>IDiaSymbol::get_noInline
检索一个标志，指定是否已标记为不被内联函数 (使用[noinline](/cpp/cpp/noinline)属性)。

## <a name="syntax"></a>语法

```C++
HRESULT get_noInline(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out]返回`TRUE`如果函数具有`noinline`属性; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [noinline](/cpp/cpp/noinline)