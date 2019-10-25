---
title: IDiaPropertyStorage：： ReadDWORD |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadDWORD
ms.assetid: 5f4c034e-a9d3-4560-94b5-ede524741439
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1764ec83a69dcc5daff267767594473bf690b341
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742913"
---
# <a name="idiapropertystoragereaddword"></a>IDiaPropertyStorage::ReadDWORD
读取属性集中 `DWORD` 值。

## <a name="syntax"></a>语法

```C++
HRESULT ReadDWORD ( 
   PROPID id,
   DWORD* pValue
);
```

#### <a name="parameters"></a>参数
 `id`

中要读取的属性的标识符（`PROPID` 在 WTypes 中定义为 `ULONG`）。

 `pValue`

弄返回属性值。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。 如果属性不是类型 `DWORD`，则返回 `E_INVALIDARG`。

## <a name="remarks"></a>备注
 @No__t_0 由 Windows 定义为32位无符号整数。

## <a name="see-also"></a>请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)