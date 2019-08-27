---
title: IDiaSymbol::get_liveRangeLength |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_liveRangeLength
ms.assetid: ffcce3cc-085c-44eb-8145-46e3819c54f9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2c85288902d1a8c75b067bec0c77242e9a246561
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64808245"
---
# <a name="idiasymbolgetliverangelength"></a>IDiaSymbol::get_liveRangeLength
返回本地符号无效的地址范围的长度。

## <a name="syntax"></a>语法

```C++
HRESULT get_liveRangeLength ( 
   ULONGLONG* length
);
```

#### <a name="parameters"></a>参数
 `length`

[out]返回的地址范围的长度。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

> [!NOTE]
> 返回的错误代码表示符号不具有实时范围信息。

## <a name="remarks"></a>备注

## <a name="requirements"></a>要求
 标头：dia2.h

 库： diaguids.lib

 DLL: msdia100.dll

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)