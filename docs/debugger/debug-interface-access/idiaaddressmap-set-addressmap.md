---
title: IDiaAddressMap::set_addressMap | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::set_addressMap method
ms.assetid: 81e82073-089b-43d5-af39-49d7a4907c7a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8414788af44d78943088b78b2d3e42a5a8d8c50b
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745032"
---
# <a name="idiaaddressmapset_addressmap"></a>IDiaAddressMap::set_addressMap
提供用于支持图像布局翻译的地址映射。

## <a name="syntax"></a>语法

```C++
HRESULT set_addressMap ( 
   DWORD                     cbData,
   struct DiaAddressMapEntry data[],
   BOOL                      imagetoSymbols
);
```

#### <a name="parameters"></a>参数
 `cbData`

中@No__t_0 参数中的元素数目。

 `data[]`

中定义平移映射的[DiaAddressMapEntry 结构](../../debugger/debug-interface-access/diaaddressmapentry.md)结构的数组。

 `imagetoSymbols`

[in] 如果 `data` 参数定义了从新图像布局到原始布局的映射（如调试符号所述），则 `TRUE`。 如果 `data` 是从原始布局获取的新图像布局的映射，则 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 通常，DIA 从程序数据库（.pdb）文件中检索地址转换映射。 如果缺少这些值，则会调用[IDiaAddressMap：： set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)方法两次，一次将 `imagetoSymbols` 参数设置为 `TRUE`，将 `imagetoSymbols` 参数设置为 `FALSE`。 除非同时提供两个翻译映射，否则无法使用[IDiaAddressMap：:P ut_addressmapenabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)方法启用地址映射转换。

## <a name="see-also"></a>请参阅
- [DiaAddressMapEntry 结构](../../debugger/debug-interface-access/diaaddressmapentry.md)
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)
- [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)