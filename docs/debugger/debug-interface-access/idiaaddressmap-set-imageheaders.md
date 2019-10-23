---
title: IDiaAddressMap：： set_imageHeaders |Microsoft Docs
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
ms.openlocfilehash: ef17e1073c67ede75d075b18773129c287349c0d
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745018"
---
# <a name="idiaaddressmapset_imageheaders"></a>IDiaAddressMap::set_imageHeaders
设置图像标头以启用相对虚拟地址转换。

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

中标头数据的字节数。 必须 `n*sizeof(IMAGE_SECTION_HEADER)`，其中 `n` 是可执行文件中的节标头的数目。

 data[]

中要用作图像标头的 `IMAGE_SECTION_HEADER` 结构的数组。

 originalHeaders

中如果图像标头来自新图像，则设置为 `FALSE`，`TRUE` 是否在升级之前反映原始映像。 通常情况下，此设置为仅 `TRUE` 结合[IDiaAddressMap：： set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)方法的调用。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 @No__t_0 结构在 Winnt 中声明，表示可执行文件的图像节标头格式。

 相对虚拟地址的计算取决于 `IMAGE_SECTION_HEADER` 值。 通常，DIA 从程序数据库（.pdb）文件中检索这些文件。 如果缺少这些值，DIA 将无法计算相对虚拟地址， [IDiaAddressMap：： get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)方法返回 `FALSE`。 然后，客户端必须调用[IDiaAddressMap：:P ut_relativevirtualaddressenabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)方法，以便在提供图像本身缺少的图像标头后启用相对虚拟地址计算。

## <a name="see-also"></a>请参阅
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
- [IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)
- [IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)