---
title: 'Idiasymbol:: Get_inlspec |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_InlSpec method
ms.assetid: 30af6a2f-be84-429e-a96a-d0f9ed9343fb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8860668452a22413db8c6fc3d0fdc664c7ba36dd
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64835389"
---
# <a name="idiasymbolgetinlspec"></a>IDiaSymbol::get_InlSpec
此函数可检索一个标志，指示是否已标记为内联的函数 (使用之一[inline、 __inline、 \__forceinline](/cpp/cpp/inline-functions-cpp)属性)。

## <a name="syntax"></a>语法

```C++
HRESULT get_inlSpec(
   BOOL *pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`如果该函数被标记为内联; 否则，返回`FALSE`。

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
- [inline、__inline、\__forceinline](/cpp/cpp/inline-functions-cpp)