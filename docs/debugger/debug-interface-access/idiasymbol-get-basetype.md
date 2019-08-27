---
title: IDiaSymbol::get_baseType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_baseType method
ms.assetid: 5c69a241-a8d3-48ed-8b36-27463a196572
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e1d38e39fd7687de3ff87737b49972cb389187aa
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62837602"
---
# <a name="idiasymbolgetbasetype"></a>IDiaSymbol::get_baseType
检索此符号的基类型<em>。</em>

## <a name="syntax"></a>语法

```C++
HRESULT get_baseType (
    DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
`pRetVal`

[out]返回一个值从[BasicType 枚举](../../debugger/debug-interface-access/basictype.md)指定符号的基类型的枚举。

## <a name="return-value"></a>返回值
如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="remarks"></a>备注
可通过首先获取符号的类型，然后询问的返回类型的基类型确定符号的基本类型。 请注意，某些符号可能不具有基类型，例如，结构名称。

## <a name="example"></a>示例

```C++
IDiaSymbol* pType;
CComPtr<IDiaSymbol> pBaseType;
if (pType->get_type( &pBaseType ) == S_OK)
{
    BasicType btBaseType;
    if (pBaseType->get_baseType((DWORD *)&btBaseType) == S_OK)
    {
        // Do something with basic type.
    }
}
```

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [BasicType 枚举](../../debugger/debug-interface-access/basictype.md)
- [IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)
