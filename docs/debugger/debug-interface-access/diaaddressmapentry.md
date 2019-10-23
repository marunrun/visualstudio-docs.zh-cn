---
title: DiaAddressMapEntry | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- DiaAddressMapEntry enumeration
ms.assetid: 5d0ae226-981d-4541-a801-fc4993fe663b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 54b326116b1e1b677a997b264cf0c168a93febb0
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745255"
---
# <a name="diaaddressmapentry"></a>DiaAddressMapEntry
描述地址映射中的条目。

## <a name="syntax"></a>语法

```C++
struct DiaAddressMapEntry {
    DWORD rva,
    DWORD rvaTo
};
```

## <a name="elements"></a>元素
`rva` 映像 A 中的相对虚拟地址（RVA）。

`rvaTo` 相对虚拟地址 `rva` 映射到的图像为 B。

## <a name="remarks"></a>备注
地址映射提供从一个图像布局（A）到另一个（B）的转换。 @No__t_0 结构的数组，该数组按 `rva` 定义地址映射。

若要将地址（`addrA`）转换为地址，请 `addrB`，在图像 B 中，执行以下步骤：

1. 在地图中搜索条目 "`e`"，其最大 `rva` 小于或等于 "`addrA`"。

2. 设置 `delta = addrA - e.rva`。

3. 设置 `addrB = e.rvaTo + delta`。

    @No__t_0 结构的数组将传递给[IDiaAddressMap：： set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)方法。

## <a name="requirements"></a>要求
标头： dia2

## <a name="see-also"></a>请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
