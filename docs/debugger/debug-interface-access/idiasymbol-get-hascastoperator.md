---
title: 'Idiasymbol:: Get_hascastoperator |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasCastOperator method
ms.assetid: a21114a6-56a3-4e8a-a65f-58ec2a0a8908
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3e8345e722036e90ebedf51ec91e274770887e49
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64808193"
---
# <a name="idiasymbolgethascastoperator"></a>IDiaSymbol::get_hasCastOperator
检索指定用户定义数据类型是否具有任何强制转换运算符定义的标志。

## <a name="syntax"></a>语法

```C++
HRESULT get_hasCastOperator ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`如果用户定义数据类型具有任何强制转换运算符定义; 否则，返回`FALSE`。

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