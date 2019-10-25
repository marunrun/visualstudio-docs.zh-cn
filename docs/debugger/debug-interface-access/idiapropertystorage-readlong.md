---
title: IDiaPropertyStorage::ReadLONG | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadLONG
ms.assetid: 32054cbc-db55-4513-a1b4-de80e77aac8a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: af9d65c571c5e0a281b968d922c9b5170bd1c561
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742893"
---
# <a name="idiapropertystoragereadlong"></a>IDiaPropertyStorage::ReadLONG
读取属性集中 `LONG` 值。

## <a name="syntax"></a>语法

```C++
HRESULT ReadDLONG ( 
   PROPID id,
   LONG*  pValue
);
```

#### <a name="parameters"></a>参数
 `id`

中要读取的属性的标识符（`PROPID` 在 WTypes 中定义为 `ULONG`）。

 `pValue`

弄返回属性值。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。 如果属性不是类型 `LONG`，则返回 `E_INVALIDARG`。

## <a name="remarks"></a>备注
 @No__t_0 由 Windows 定义为32位有符号整数。

## <a name="see-also"></a>请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)