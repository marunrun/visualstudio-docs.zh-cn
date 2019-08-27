---
title: IDiaSymbol::get_addressSection | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_addressSection method
ms.assetid: fe80d479-3bb5-4f55-9b62-1bd58d0a60ce
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f4ae24a194050868e1e2efbc5d29e7cf20e6cf5d
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64830591"
---
# <a name="idiasymbolgetaddresssection"></a>IDiaSymbol::get_addressSection
检索的部分一部分的地址位置。 何时使用[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)设置为`LocIsStatic`。

## <a name="syntax"></a>语法

```C++
HRESULT get_addressSection ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回地址位置部分的部分。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="remarks"></a>备注
 对于位于外部 DLL 中的静态成员，此方法返回的部分可能为 0，因为此方法依赖于获取成员的虚拟地址。 虚拟地址都有效才[idiasession:: Put_loadaddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)中的方法[IDiaSession](../../debugger/debug-interface-access/idiasession.md)已使用指定的 dll 加载地址的非零参数调用接口。

 若要获取地址的偏移量的部分，请调用[idiasymbol:: Get_addressoffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)方法。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)