---
title: IDiaPropertyStorage：： ReadULONGLONG |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadULONGLONG
ms.assetid: f80a2e24-5744-4fec-bab0-3ed51aef6e58
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dde2f111e468b8ccf6c1d91440f06d3e7048a0f6
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742856"
---
# <a name="idiapropertystoragereadulonglong"></a>IDiaPropertyStorage::ReadULONGLONG
读取属性集中 `ULONGLONG` 值。

## <a name="syntax"></a>语法

```C++
HRESULT ReadULONGLONG ( 
   PROPID     id,
   ULONGLONG* pValue
);
```

#### <a name="parameters"></a>参数
 `id`

中要读取的属性的标识符（`PROPID` 在 WTypes 中定义为 `ULONG`）。

 `pValue`

弄返回属性值。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。 如果属性不是类型 `ULONGLONG`，则返回 `E_INVALIDARG`。

## <a name="remarks"></a>备注
 @No__t_0 由 Windows 定义为64位无符号整数。

## <a name="see-also"></a>请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)