---
title: IDiaAddressMap::get_relativeVirtualAddressEnabled | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::get_relativeVirtualAddressEnabled method
ms.assetid: 4c48af81-7148-4d9a-818e-dbe62cbfc638
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 72ea881470eb3cfbb1c544324218b122a4470efc
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745190"
---
# <a name="idiaaddressmapget_relativevirtualaddressenabled"></a>IDiaAddressMap::get_relativeVirtualAddressEnabled
指示是否启用了相对虚拟地址（RVA）的计算和使用。

## <a name="syntax"></a>语法

```C++
HRESULT get_relativeVirtualAddressEnabled ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 pRetVal

弄如果启用了 Rva 计算，则返回 `TRUE`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 如果已从 PDB 文件中最初加载段，则启用 Rva。 可以通过调用[IDiaAddressMap：:P ut_relativevirtualaddressenabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)方法来暂时禁用 rva 的使用。

 此外，还可以通过调用[IDiaAddressMap：： set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)方法，然后调用 `put_relativeVirtualAddressEnabled` 方法来建立新的图像标头，以便能够使用新的图像标头来使用 rva。

## <a name="see-also"></a>请参阅
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)
- [IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)