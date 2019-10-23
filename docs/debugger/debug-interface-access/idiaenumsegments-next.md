---
title: IDiaEnumSegments::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Next method
ms.assetid: 53f61874-d821-47ab-a1f5-27e982804a6a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 34062b654cbaccec053c5ac50bfb041d37a0f4e6
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744193"
---
# <a name="idiaenumsegmentsnext"></a>IDiaEnumSegments::Next
检索枚举序列中指定数量的段。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
   ULONG         celt,
   IDiaSegment** rgelt,
   ULONG*        pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

中要检索的枚举数中的段数。

 rgelt

弄要使用表示段的所需[IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)对象填充的数组。

 pceltFetched

弄返回提取的枚举数中的段数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有其他段，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)