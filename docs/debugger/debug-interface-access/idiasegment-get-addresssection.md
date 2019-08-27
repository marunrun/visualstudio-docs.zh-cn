---
title: IDiaSegment::get_addressSection | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSegment::get_addressSection method
ms.assetid: 360b61b1-69b1-4a8b-ba37-97a1d835ac53
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2e098f1e2367395f201abf6f44554f1699400b12
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827795"
---
# <a name="idiasegmentgetaddresssection"></a>IDiaSegment::get_addressSection
检索映射到此段的节号。

## <a name="syntax"></a>语法

```C++
HRESULT get_addressSection ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回映射到此段的部分数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)