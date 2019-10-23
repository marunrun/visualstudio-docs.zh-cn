---
title: IDiaPropertyStorage::ReadBOOL | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadBOOL
ms.assetid: ad1822db-4572-48f7-9919-f8137f6701f2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d776e37bab189e61d0264f4cbda24f89cb4501ce
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742927"
---
# <a name="idiapropertystoragereadbool"></a>IDiaPropertyStorage::ReadBOOL
读取属性集中 `BOOL` 值。

## <a name="syntax"></a>语法

```C++
HRESULT ReadBOOL ( 
   PROPID id,
   BOOL*  pValue
);
```

#### <a name="parameters"></a>参数
 `id`

中要读取的属性的标识符（`PROPID` 在 WTypes 中定义为 `ULONG`）。

 `pValue`

弄返回属性值。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。 如果属性不是类型 `BOOL`，则返回 `E_INVALIDARG`。

## <a name="remarks"></a>备注
 为了保持一致的结果，请将 `BOOL` 值解释为 `TRUE` 零值，`FALSE` 为零。

## <a name="see-also"></a>请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)