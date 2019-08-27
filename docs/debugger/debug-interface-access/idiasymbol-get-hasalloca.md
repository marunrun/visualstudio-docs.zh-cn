---
title: IDiaSymbol::get_hasAlloca | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasAlloca method
ms.assetid: 3b9fb747-670b-4da7-bb70-612f7b911786
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 457f446af4a91141962fbbd3055d9ce4980c719a
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64808788"
---
# <a name="idiasymbolgethasalloca"></a>IDiaSymbol::get_hasAlloca
检索一个标志，指定该函数是否包含对的调用`alloca`（这用于在堆栈上分配内存）。

## <a name="syntax"></a>语法

```cpp
HRESULT get_hasAlloca(   BOOL *pFlag);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out]返回`TRUE`如果该函数包含对的调用`alloca`; 否则为返回`FALSE`。

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