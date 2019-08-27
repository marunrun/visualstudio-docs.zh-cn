---
title: IDiaSymbol::get_age | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_age method
ms.assetid: 60d05654-e832-4a2e-a4a7-fe9922c459fe
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4e35db1186f2547b8d3c859d20e0e4ce2b1f68e9
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64803347"
---
# <a name="idiasymbolgetage"></a>IDiaSymbol::get_age
检索一个.pdb 文件的年龄值。

## <a name="syntax"></a>语法

```C++
HRESULT get_age ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回一个.pdb 文件的年龄值。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="remarks"></a>备注
 为任何已知的时间值; 不一定对应年龄它通常用于确定是否与相应的.exe 文件不同步的.pdb 文件。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)