---
title: 'Idiasymbol:: Get_isstatic |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isStatic method
ms.assetid: 3be5fe1b-46e8-4b07-90d8-4929dbbe7ff7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 50c19104d0597c9aa178569d0d103bb3e57f18ed
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64813383"
---
# <a name="idiasymbolgetisstatic"></a>IDiaSymbol::get_isStatic
检索一个标志，指定是否在函数或 thunk 层已标记为静态。

## <a name="syntax"></a>语法

```C++
HRESULT get_isStatic(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out]返回`TRUE`函数或 thunk 层已标记为静态的; 否则为如果返回`FALSE`。

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