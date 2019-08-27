---
title: IDiaLoadCallback2::RestrictDBGAccess | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback2::RestrictDBGAccess method
ms.assetid: 63b67a93-2910-4fff-aa70-6b2eaa08e5c8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 24317ff7a79815e5af2306b09cc8d2aa3bfdde0d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832649"
---
# <a name="idialoadcallback2restrictdbgaccess"></a>IDiaLoadCallback2::RestrictDBGAccess
确定从.dbg 文件是否允许查找调试信息。

## <a name="syntax"></a>语法

```C++
HRESULT RestrictDBGAccess();
```

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 任何返回值而不`S_OK`以免寻找.dbg 文件中的调试信息。

## <a name="see-also"></a>请参阅
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)