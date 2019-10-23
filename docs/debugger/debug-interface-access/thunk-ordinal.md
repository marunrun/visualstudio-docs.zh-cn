---
title: THUNK_ORDINAL | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Thunk_Ordinal enumeration
ms.assetid: 026f98a9-36b8-41ef-8a72-12d7cbc2d362
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1de2d6c9700dcb7b1106c3693d855bb1d8ae2cfa
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738499"
---
# <a name="thunk_ordinal"></a>THUNK_ORDINAL
指定 thunk 类型。

## <a name="syntax"></a>语法

```C++
typedef enum THUNK_ORDINAL {
    THUNK_ORDINAL_NOTYPE,
    THUNK_ORDINAL_ADJUSTOR,
    THUNK_ORDINAL_VCALL,
    THUNK_ORDINAL_PCODE,
    THUNK_ORDINAL_LOAD

    // trampoline thunk ordinals - only for use in Trampoline thunk symbols
    THUNK_ORDINAL_TRAMP_INCREMENTAL,
    THUNK_ORDINAL_TRAMP_BRANCHISLAND,
} THUNK_ORDINAL;
```

## <a name="elements"></a>元素
THUNK_ORDINAL_NOTYPE 标准 thunk。

THUNK_ORDINAL_ADJUSTOR `this` ADJUSTOR thunk。

THUNK_ORDINAL_VCALL 虚拟调用 thunk。

THUNK_ORDINAL_PCODE P-代码形式。

THUNK_ORDINAL_LOAD 延迟加载 thunk。

THUNK_ORDINAL_TRAMP_INCREMENTAL 增量 trampoline thunk （trampoline thunk 用于弹跳从一个内存空间到另一个内存空间的调用）。

THUNK_ORDINAL_TRAMP_BRANCHISLAND 分支点 trampoline thunk。

## <a name="remarks"></a>备注
此枚举中的值从对[IDiaSymbol：： get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)方法的调用返回。

## <a name="requirements"></a>要求
标头： cvconst

## <a name="see-also"></a>请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)
