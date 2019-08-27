---
title: IDiaSymbol::get_hasSEH | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasSEH method
ms.assetid: 1a709ded-22c8-464c-97be-eba5e464210c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 41987007dd5121dff8cce1eb91ea9e1c4d93578c
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64816344"
---
# <a name="idiasymbolgethasseh"></a>IDiaSymbol::get_hasSEH
检索一个标志，指定该函数是否包含任何[结构化异常处理 (C /C++)](/cpp/cpp/structured-exception-handling-c-cpp) (例如，__try /\__except 块)。

## <a name="syntax"></a>语法

```C++
HRESULT get_hasSEH(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out]返回`TRUE`如果函数具有任何结构化的异常处理块; 否则，返回`FALSE`。

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
- [结构化异常处理 (C/C++)](/cpp/cpp/structured-exception-handling-c-cpp)