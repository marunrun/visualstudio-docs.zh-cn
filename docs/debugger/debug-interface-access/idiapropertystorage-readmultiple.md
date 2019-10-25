---
title: IDiaPropertyStorage：： ReadMultiple |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadMultiple
ms.assetid: 6ccc9397-ce41-4f72-b261-72ac252cd4a5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9cd1e419e1d08120274fc627a672eb52331ca50f
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742876"
---
# <a name="idiapropertystoragereadmultiple"></a>IDiaPropertyStorage::ReadMultiple
从当前属性集中读取指定的属性。

## <a name="syntax"></a>语法

```C++
HRESULT ReadMultiple( 
   ULONG          cpspec,
   PROPSPEC const rgpspec,
   PROPVARIANT    rgvar
);
```

#### <a name="parameters"></a>参数
 `cpspec`

中@No__t_0 数组中指定的属性计数。 如果为零，则此方法不返回任何属性，但会返回 `S_OK` 作为成功代码。

 `rgpspec`

中要读取的属性的数组。 可以通过属性 ID 或可选的字符串名称指定属性。 不需要在数组中按任何特定顺序指定属性。 数组可以包含重复的属性，导致简单属性返回时出现重复的属性值。 非简单属性应返回拒绝访问，尝试再次打开它们。 数组可以包含属性 Id 和字符串 Id 的混合。 此数组必须具有至少 `cpspec` 属性值的数目。

 `rgvar`

[in，out]要为其填充每个属性的值的 `PROPVARIANT` 结构的数组（在 VisualStudio 命名空间中）。 数组的大小必须至少为 `cpspec` 元素。 调用方不需要初始化数组中的值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果找不到一个或多个属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 如果找不到属性，则 `rgvar` 数组中的相应条目包含具有 `VT_EMPTY` 类型的 `VARIANT`。

## <a name="see-also"></a>请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)