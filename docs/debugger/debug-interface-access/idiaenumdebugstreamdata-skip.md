---
title: 'Idiaenumdebugstreamdata:: Skip |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreamData::Skip method
ms.assetid: 106ae1d3-a379-4077-babf-2665e697b0c4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 61c33ab75ebac94ec69d772ae23476df28bdb31d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62838358"
---
# <a name="idiaenumdebugstreamdataskip"></a>IDiaEnumDebugStreamData::Skip
将跳过指定的数目的枚举序列中的记录。

## <a name="syntax"></a>语法

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>参数
 celt

[in]要跳过枚举序列中的记录数。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`如果没有更多记录要跳过。

## <a name="see-also"></a>请参阅
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)