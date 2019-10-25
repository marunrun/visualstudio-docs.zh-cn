---
title: IDiaEnumSegments::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Item method
ms.assetid: ee44dd55-39a0-4b7b-97ff-2e1226eeb2bd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 101821e3c00d3aeac9b131ee5a11ab9a01e090a9
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744187"
---
# <a name="idiaenumsegmentsitem"></a>IDiaEnumSegments::Item
通过索引检索段。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   DWORD         index,
   IDiaSegment** segment
);
```

#### <a name="parameters"></a>参数
 索引

中要检索的[IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)对象的索引。 索引的范围为0到 `count`-1，其中 `count` 由[IDiaEnumSegments：： get_Count](../../debugger/debug-interface-access/idiaenumsegments-get-count.md)方法返回。

 段

弄返回一个[IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)对象，该对象表示所需的段。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)