---
title: IDiaSymbol::get_registerId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_registerId method
ms.assetid: f881e793-eb9e-48dc-a847-dd61d77174fc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3e2b1cbb6837ca139e735bef17bc0c2712d9cae7
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64786586"
---
# <a name="idiasymbolgetregisterid"></a>IDiaSymbol::get_registerId
检索到的位置的注册指示符时[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)设置为`LocIsEnregistered`。

## <a name="syntax"></a>语法

```C++
HRESULT get_registerId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回位置的注册指示符。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="remarks"></a>备注
 如果符号为相对于寄存器，也就是说，如果符号[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)设置为`LocIsRegRel`，使用`get_registerId`方法后调用[idiasymbol:: Get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md)若要获取从符号所在的位置的寄存器的偏移量的方法。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)