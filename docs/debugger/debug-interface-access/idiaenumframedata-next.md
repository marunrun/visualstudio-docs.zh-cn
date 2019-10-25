---
title: IDiaEnumFrameData：： Next |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::Next method
ms.assetid: 546e2e23-efb2-425a-96a1-808c67c519fb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6fe478e503ed6e16ee570f309f91434c658ebd27
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744601"
---
# <a name="idiaenumframedatanext"></a>IDiaEnumFrameData::Next
检索枚举序列中指定数目的帧数据元素。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
   ULONG           celt,
   IDiaFrameData** rgelt,
   ULONG*          pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

中枚举器中要检索的帧数据元素的数目。

 rgelt

弄要使用请求的帧数据元素填充的[IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)对象数组。

 pceltFetched

弄返回提取的枚举器中的帧数据元素数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多记录，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)