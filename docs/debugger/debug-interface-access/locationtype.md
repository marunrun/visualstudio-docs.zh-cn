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
ms.openlocfilehash: dc40cc6cc8e821db7c28a4647e36e7bad241b29f
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738637"
---
# <a name="locationtype"></a>LocationType
指示符号中包含的位置信息类型。

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

`LocIsTLS` 位置在线程本地存储中。

`LocIsRegRel` 位置是寄存器相关的。

`LocIsThisRel` 位置是 `this` 相关的。

`LocIsEnregistered` 位置位于寄存器中。

`LocIsBitField` 位置在位域中。

`LocIsSlot` 位置是 Microsoft 中间语言（MSIL）槽。

`LocIsIlRel` 位置是 MSIL 相关的。

`LocInMetaData` 位置在元数据中。

`LocIsConstant` 位置在常量值中。

`LocTypeMax` 此枚举中的位置类型的数目。

## <a name="remarks"></a>备注
[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)接口可用的属性取决于该符号在图像文件中的位置。 有关详细信息，请参阅[符号位置](../../debugger/debug-interface-access/symbol-locations.md)。

此枚举中的值由对[IDiaSymbol：： get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)方法的调用返回。

## <a name="requirements"></a>要求
标头： cvconst

## <a name="see-also"></a>请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)
- [符号位置](../../debugger/debug-interface-access/symbol-locations.md)
