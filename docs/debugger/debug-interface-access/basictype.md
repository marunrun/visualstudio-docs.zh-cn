---
title: BasicType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- BasicType enumeration
ms.assetid: 19ae53ba-cd6e-47b6-9f94-27ae663ce955
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3fff76abdecdd8613a462225278053ef4f6d9694
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745478"
---
# <a name="basictype"></a>BasicType
指定符号的基本类型。

## <a name="syntax"></a>语法

```C++
enum BasicType {
    btNoType   = 0,
    btVoid     = 1,
    btChar     = 2,
    btWChar    = 3,
    btInt      = 6,
    btUInt     = 7,
    btFloat    = 8,
    btBCD      = 9,
    btBool     = 10,
    btLong     = 13,
    btULong    = 14,
    btCurrency = 25,
    btDate     = 26,
    btVariant  = 27,
    btComplex  = 28,
    btBit      = 29,
    btBSTR     = 30,
    btHresult  = 31,
    btChar16   = 32,  // char16_t
    btChar32   = 33,  // char32_t
};
```

## <a name="elements"></a>元素
btNoType 未指定基本类型。

btVoid 基本类型为 `void`。

btChar 基本类型是 `char` （C/C++类型）。

btWChar Basic type 是宽（Unicode）字符（`WCHAR`）。

btInt 基本类型为 `signed int` （C/C++ type）。

btUInt 基本类型为 `unsigned int` （C/C++ type）。

btFloat 基本类型为浮点数（`FLOAT`）。

btBCD 基本类型是二进制编码的十进制数（`BCD`）。

btBool 基本类型为布尔值（`BOOL`）。

btLong 基本类型是 `long int` （C/C++类型）。

btULong 基本类型是 `unsigned long int` （C/C++类型）。

btCurrency 基本类型为 currency。

btDate 基本类型是日期/时间（`DATE`）。

btVariant Basic type 是变量类型结构（`VARIANT`）。

btComplex 基本类型为复数。

btBit 基本类型有点如此。

btBSTR 基本类型是基本或二进制字符串（`BSTR`）。

btHresult 基本类型为 `HRESULT`。

## <a name="remarks"></a>备注
此枚举中的值由[IDiaSymbol：： get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md)方法返回。

## <a name="requirements"></a>要求
标头： cvconst

## <a name="see-also"></a>请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md)
- [IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)
