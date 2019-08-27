---
title: 'Idiasymbol:: Get_length |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_length method
ms.assetid: cc62f028-d195-4fbf-93bc-10b08bef52d2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7b1a583a9afd2a43d48399d5e2787369ab9bef95
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64858108"
---
# <a name="idiasymbolgetlength"></a>IDiaSymbol::get_length
检索比特数或通过此符号表示的对象使用的内存字节数。

## <a name="syntax"></a>语法

```C++
HRESULT get_length ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回的字节数或 bits 通过此符号表示的对象使用的内存。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="remarks"></a>备注
 如果[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)的符号是`LocIsBitField`，此方法返回的长度是以位为单位; 否则，长度是以字节为单位的所有其他位置类型。

## <a name="example"></a>示例

```C++
IDiaSymbol* pSymbol;
ULONGLONG   length;
pSymbol->get_length( &length );
```

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)