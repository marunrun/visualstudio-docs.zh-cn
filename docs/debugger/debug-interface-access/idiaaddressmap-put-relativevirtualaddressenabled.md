---
title: 'Idiaaddressmap:: Put_relativevirtualaddressenabled |Microsoft Docs'
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
ms.openlocfilehash: 371db781cae5c988e6c8ff4c4776c5f43d6f047a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62554347"
---
# <a name="idiaaddressmapputrelativevirtualaddressenabled"></a>IDiaAddressMap::put_relativeVirtualAddressEnabled
允许客户端启用或禁用的计算和使用的相对虚拟地址 (RVA)。

## <a name="syntax"></a>语法

```C++
HRESULT put_relativeVirtualAddressEnabled ( 
   BOOL NewVal
);
```

#### <a name="parameters"></a>参数
 NewVal

[in]设置为`TRUE`若要启用，或`FALSE`禁用。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 作为相对虚拟地址，可以检索通过 DIA 接口，以及相对于基可执行文件的图像所述的调试对象的地址。

 Rva 被启用从 PDB 文件最初加载段。 若要获取的 Rva 使用的当前状态，请调用[idiaaddressmap:: Get_relativevirtualaddressenabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)方法。

 `put_relativeVirtualAddress`必须在调用方法是在成功调用之后启用 Rva [idiaaddressmap:: Set_imageheaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)方法已建立新的映像标头。

## <a name="see-also"></a>请参阅
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)
- [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)