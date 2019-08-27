---
title: 'Idiasymbol:: Get_noreturn |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_noReturn method
ms.assetid: 704c1cc0-5b84-4334-a02a-70f43aff39d5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0857939289091d22aaafb5dc5bb009d4af0e00bb
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64830295"
---
# <a name="idiasymbolgetnoreturn"></a>IDiaSymbol::get_noReturn
检索一个标志，该函数是否已标记为永远不会返回具有指定[noreturn](/cpp/cpp/noreturn)属性。

## <a name="syntax"></a>语法

```C++
HRESULT get_noReturn(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 pFlag

[out]返回`TRUE`如果该函数已被声明为永远不会返回具有`noreturn`属性; 否则，返回`FALSE`。

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
- [noreturn](/cpp/cpp/noreturn)