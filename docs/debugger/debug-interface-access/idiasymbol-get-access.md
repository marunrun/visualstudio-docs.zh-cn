---
title: 'Idiasymbol:: Get_access |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_access method
ms.assetid: 908976ae-95c4-4020-89c9-de137f727f98
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fcf510cd9c74e22e0d028552b26c85b1f3d59bd4
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64813917"
---
# <a name="idiasymbolgetaccess"></a>IDiaSymbol::get_access
检索的类成员的访问修饰符。

## <a name="syntax"></a>语法

```C++
HRESULT get_access ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回一个值从[CV_access_e 枚举](../../debugger/debug-interface-access/cv-access-e.md)枚举，用于指定类成员的访问修饰符。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [CV_access_e 枚举](../../debugger/debug-interface-access/cv-access-e.md)