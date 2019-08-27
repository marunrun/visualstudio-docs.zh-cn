---
title: IDiaSymbol::get_liveRangeStartAddressSection | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_liveRangeStartAddressSection
ms.assetid: 892b80ff-5957-4233-b4d7-6144167be289
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c99b5a14a321a28bdbe7337dcc7cdfa5febdad5d
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64786527"
---
# <a name="idiasymbolgetliverangestartaddresssection"></a>IDiaSymbol::get_liveRangeStartAddressSection
返回的部分一部分的本地符号的范围的起始地址。

## <a name="syntax"></a>语法

```C++
HRESULT get_liveRangeStartAddressSection ( 
   DWORD* section
);
```

#### <a name="parameters"></a>参数
 `section`

[out]返回起始地址范围部分的部分。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

> [!NOTE]
> 返回的错误代码表示符号不具有实时范围信息。

## <a name="remarks"></a>备注
 通过部分和偏移量而形成的地址是范围的符号无效的开头。

 若要获取地址的偏移量的部分，请使用[IDiaSymbol::get_liveRangeStartAddressOffset](../../debugger/debug-interface-access/idiasymbol-get-liverangestartaddressoffset.md)。

## <a name="requirements"></a>要求
 标头：dia2.h

 库： diaguids.lib

 DLL: msdia100.dll

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)