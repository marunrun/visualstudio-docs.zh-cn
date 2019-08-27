---
title: LocationType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- LocationType enumeration
ms.assetid: d3e1eedc-bfd3-4c91-881b-d69565138d0f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: faff61833cb130902efbd64d60a16f74c507a3e2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62834124"
---
# <a name="locationtype"></a>LocationType
指示符号中包含的位置信息的类型。

## <a name="syntax"></a>语法

```C++
enum LocationType {
    LocIsNull,
    LocIsStatic,
    LocIsTLS,
    LocIsRegRel,
    LocIsThisRel,
    LocIsEnregistered,
    LocIsBitField,
    LocIsSlot,
    LocIsIlRel,
    LocInMetaData,
    LocIsConstant,
    LocTypeMax
};
```

## <a name="elements"></a>元素
`LocIsNull` 位置信息不可用。

`LocIsStatic` 位置是静态的。

`LocIsTLS` 位置是在线程本地存储中。

`LocIsRegRel` 位置是寄存器相对。

`LocIsThisRel` 位置是`this`-相对。

`LocIsEnregistered` 位置是在寄存器中。

`LocIsBitField` 位置所在的位字段。

`LocIsSlot` 位置是 Microsoft 中间语言 (MSIL) 槽。

`LocIsIlRel` 位置是 MSIL 相对。

`LocInMetaData` 位置是在元数据中。

`LocIsConstant` 位置是常量值。

`LocTypeMax` 此枚举中的位置类型的数。

## <a name="remarks"></a>备注
可使用的属性[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)接口取决于图像文件中的符号的位置。 有关详细信息，请参阅[符号位置](../../debugger/debug-interface-access/symbol-locations.md)。

此枚举中的值返回通过调用[idiasymbol:: Get_locationtype](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)方法。

## <a name="requirements"></a>要求
标头： cvconst.h

## <a name="see-also"></a>请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)
- [符号位置](../../debugger/debug-interface-access/symbol-locations.md)
