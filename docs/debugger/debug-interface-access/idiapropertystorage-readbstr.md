---
title: IDiaPropertyStorage：： ReadBSTR |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadBSTR
ms.assetid: 7214643b-3286-48ed-90aa-0fe95b4cae5b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ef0b5bac11a1bf3da7e8081f7ae24b6a7a6f1a71
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742916"
---
# <a name="idiapropertystoragereadbstr"></a>IDiaPropertyStorage::ReadBSTR
读取属性集中 `BSTR` 值。

## <a name="syntax"></a>语法

```C++
HRESULT ReadBSTR ( 
   PROPID id,
   BSTR*  pValue
);
```

#### <a name="parameters"></a>参数
 `id`

中要读取的属性的标识符（`PROPID` 在 WTypes 中定义为 `ULONG`）。

 `pValue`

弄返回属性值。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。 如果属性不是类型 `BSTR`，则返回 `E_INVALIDARG`。

## <a name="remarks"></a>备注
 @No__t_0 由 Windows 定义为以零结尾的宽字符字符串。

## <a name="see-also"></a>请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)