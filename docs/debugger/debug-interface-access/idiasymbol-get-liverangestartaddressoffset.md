---
title: IDiaSymbol::get_liveRangeStartAddressOffset | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_liveRangeStartAddressOffset
ms.assetid: f5b28914-0a14-4b22-8259-59d7f97ee610
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0312571b0a96b080949398618888b05c2704d3ca
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64808941"
---
# <a name="idiasymbolgetliverangestartaddressoffset"></a>IDiaSymbol::get_liveRangeStartAddressOffset
返回本地符号的范围的起始地址的偏移量的部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_liveRangeStartAddressOffset ( 
   DWORD* offset
);
```

#### <a name="parameters"></a>参数
 `offset`

[out]返回的起始地址范围的偏移量的部分。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

> [!NOTE]
> 返回的错误代码表示符号不具有实时范围信息。

## <a name="remarks"></a>备注
 通过部分和偏移量而形成的地址是范围的符号无效的开头。

 若要获取的地址部分一部分，请使用[IDiaSymbol::get_liveRangeStartAddressSection](../../debugger/debug-interface-access/idiasymbol-get-liverangestartaddresssection.md)。

## <a name="requirements"></a>要求
 标头：dia2.h

 库： diaguids.lib

 DLL: msdia100.dll

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)