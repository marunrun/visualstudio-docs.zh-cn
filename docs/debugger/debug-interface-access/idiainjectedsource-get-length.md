---
title: 'Idiainjectedsource:: Get_length |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_length method
ms.assetid: 38b88b8b-c2e0-4b2d-8b8b-9ff373733e78
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8333c7e57c3cd3f240f8a72dd865e458b23bc299
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828638"
---
# <a name="idiainjectedsourcegetlength"></a>IDiaInjectedSource::get_length
检索的代码的字节数。

## <a name="syntax"></a>语法

```C++
HRESULT get_length ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回代码的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的值是对源代码的长度并与相同的值返回的[idiainjectedsource:: Get_source](../../debugger/debug-interface-access/idiainjectedsource-get-source.md)方法。

## <a name="see-also"></a>请参阅
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
- [IDiaInjectedSource::get_source](../../debugger/debug-interface-access/idiainjectedsource-get-source.md)