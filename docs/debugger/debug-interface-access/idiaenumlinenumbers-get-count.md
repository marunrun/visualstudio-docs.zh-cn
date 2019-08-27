---
title: IDiaEnumLineNumbers::get_Count | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers::get_Count method
ms.assetid: dbb55936-b754-4a27-8b82-9537a7adb664
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 33078226c0610d0d992147e2ce4bec3697e3b3ae
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829880"
---
# <a name="idiaenumlinenumbersgetcount"></a>IDiaEnumLineNumbers::get_Count
检索数目的行号。

## <a name="syntax"></a>语法

```C++
HRESULT get_Count ( 
   LONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 pRetVal

[out]返回行号的数。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaEnumLineNumbers::Item](../../debugger/debug-interface-access/idiaenumlinenumbers-item.md)