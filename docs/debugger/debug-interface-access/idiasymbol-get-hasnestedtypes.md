---
title: 'Idiasymbol:: Get_hasnestedtypes |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasNestedTypes method
ms.assetid: 1a8306bd-10dd-40a9-81fc-01f71c348484
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 61073f5630e5da7edeb761774e4ba8b4c341a8cd
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64796570"
---
# <a name="idiasymbolgethasnestedtypes"></a>IDiaSymbol::get_hasNestedTypes
检索指定用户定义数据类型是否具有嵌套类型定义的标志。

## <a name="syntax"></a>语法

```C++
HRESULT get_hasNestedTypes ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`如果用户定义数据类型有嵌套类型定义; 否则，返回`FALSE`。

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