---
title: IDiaSymbol::get_dataKind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_dataKind method
ms.assetid: 45005ad0-8b29-4cde-9d33-6bef72f6e463
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cf4a0324046383557c9c32afae2e6f05a41124ba
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64790383"
---
# <a name="idiasymbolgetdatakind"></a>IDiaSymbol::get_dataKind
检索数据符号的变量的分类。

## <a name="syntax"></a>语法

```C++
HRESULT get_dataKind ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回一个值从[DataKind 枚举](../../debugger/debug-interface-access/datakind.md)例如指定的全局、 静态的或常量，例如数据类型的枚举。

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
- [DataKind 枚举](../../debugger/debug-interface-access/datakind.md)