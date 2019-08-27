---
title: IDiaEnumSegments::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Skip method
ms.assetid: ec67039f-da8c-4e70-8db7-957d7d5281e8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ff4c5d26d875dc098775d0d379e7d12b062801cd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62840013"
---
# <a name="idiaenumsegmentsskip"></a>IDiaEnumSegments::Skip
将跳过枚举序列中的指定的段数。

## <a name="syntax"></a>语法

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>参数
 celt

[in]若要跳过枚举序列中的段的数目。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`如果没有分段可以跳过。

## <a name="see-also"></a>请参阅
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)