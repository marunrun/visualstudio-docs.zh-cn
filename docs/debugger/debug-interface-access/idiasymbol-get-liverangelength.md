---
title: IDiaSymbol：： get_liveRangeLength |Microsoft Docs
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
ms.openlocfilehash: b663ef54959544764016fe59e4b0fb41607854b1
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739931"
---
# <a name="idiasymbolget_liverangelength"></a>IDiaSymbol::get_liveRangeLength
返回本地符号有效的地址范围长度。

## <a name="syntax"></a>语法

```C++
HRESULT get_liveRangeLength ( 
   ULONGLONG* length
);
```

#### <a name="parameters"></a>参数
 `length`

弄返回地址范围的长度。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

> [!NOTE]
> 返回的错误代码表示该符号没有活动范围信息。

## <a name="remarks"></a>备注

## <a name="requirements"></a>要求
 标头： Dia2

 库： diaguids

 DLL： msdia100

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)