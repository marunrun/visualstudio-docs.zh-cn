---
title: IDiaAddressMap：:p ut_relativeVirtualAddressEnabled |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_relativeVirtualAddressEnabled method
ms.assetid: 767c078e-8ad7-4940-9e00-cae7704aadee
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1d733a51bd599b85dcc6d1121b8d21e1a687a351
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745041"
---
# <a name="idiaaddressmapput_relativevirtualaddressenabled"></a>IDiaAddressMap::put_relativeVirtualAddressEnabled
允许客户端启用或禁用相对虚拟地址（RVA）的计算和使用。

## <a name="syntax"></a>语法

```C++
HRESULT put_relativeVirtualAddressEnabled ( 
   BOOL NewVal
);
```

#### <a name="parameters"></a>参数
 NewVal

中设置为 "`TRUE`" 以启用或 `FALSE` 禁用。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 DIA 接口所描述的调试对象的地址，以及可执行文件的映像库的地址可以检索为相对虚拟地址。

 当段最初从 PDB 文件加载时，将启用 Rva。 若要获取 Rva 的当前状态，请调用[IDiaAddressMap：： get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)方法。

 必须调用 `put_relativeVirtualAddress` 方法，以便在对[IDiaAddressMap：： set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)方法的成功调用已建立新的图像标头后启用 rva。

## <a name="see-also"></a>请参阅
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)
- [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)