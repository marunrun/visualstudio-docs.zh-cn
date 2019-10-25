---
title: IDiaPropertyStorage：： ReadPropertyNames |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadPropertyNames
ms.assetid: f8bcab77-afca-4a8f-8710-697842f8a518
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f554485ae56a9d5f190c749879545165d299531c
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742871"
---
# <a name="idiapropertystoragereadpropertynames"></a>IDiaPropertyStorage::ReadPropertyNames
检索给定属性标识符对应的字符串名称。

## <a name="syntax"></a>语法

```C++
HRESULT ReadPropertyNames (
   ULONG         cpropid,
   PROPID const* rgpropid,
   BSTR*         rglpwstrName
);
```

#### <a name="parameters"></a>参数
 `cpropid`

中@No__t_0 中的属性 id 数。

 `rgpropid`

中要获取其名称的属性 id 的数组（`PROPID` 在 WTypes 中定义为 `ULONG`）。

 `rglpwstrName`

[in，out]指定的属性 id 的属性名称数组。 必须预先分配数组以容纳请求的属性名称数，并且必须能够至少容纳 `cpropid``BSTR` 字符串。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 当不再需要返回的属性名称时，必须通过调用 `SysFreeString` 函数将其释放。

## <a name="see-also"></a>请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)