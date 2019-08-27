---
title: 'Idiaaddressmap:: Set_imageheaders |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::set_imageHeaders method
ms.assetid: a46b9d0e-43e6-433f-b2c7-aa203981e4e4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 10835f422f8d2d116234eadd91da0d27c424f314
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62554217"
---
# <a name="idiaaddressmapsetimageheaders"></a>IDiaAddressMap::set_imageHeaders
设置映像标头，以便相对虚拟地址转换。

## <a name="syntax"></a>语法

```C++
HRESULT set_imageHeaders ( 
   DWORD cbData,
   BYTE  data[],
   BOOL  originalHeaders
);
```

#### <a name="parameters"></a>参数
 cbData

[in]标头数据的字节数。 必须是`n*sizeof(IMAGE_SECTION_HEADER)`其中`n`是可执行文件中的部分标头数。

 data[]

[in]一个数组`IMAGE_SECTION_HEADER`结构，以用作映像标头。

 originalHeaders

[in]设置为`FALSE`从新的映像，映像标头是否`TRUE`如果它们反映在升级之前的原始映像。 通常情况下，这将设置为`TRUE`仅在通过调用组合[idiaaddressmap:: Set_addressmap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)方法。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 `IMAGE_SECTION_HEADER`结构在 Winnt.h 中声明，表示可执行文件的图像部分标头格式。

 取决于相对虚拟地址计算`IMAGE_SECTION_HEADER`值。 通常情况下，DIA 检索这些程序数据库 (.pdb) 文件中。 如果缺少这些值，DIA 是无法计算相对虚拟地址并[idiaaddressmap:: Get_relativevirtualaddressenabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)方法将返回`FALSE`。 然后，客户端必须调用[idiaaddressmap:: Put_relativevirtualaddressenabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)方法，以提供图像本身中的缺少映像标头后使相对虚拟地址计算。

## <a name="see-also"></a>请参阅
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
- [IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)
- [IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)