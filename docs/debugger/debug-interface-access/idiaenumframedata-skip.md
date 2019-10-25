---
title: IDiaEnumFrameData：： Skip |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::Skip method
ms.assetid: 67140b4c-7125-4895-932d-42412326da29
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c49aaf1f648a52e1701088b6579eda55cde6c355
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744575"
---
# <a name="idiaenumframedataskip"></a>IDiaEnumFrameData::Skip
跳过枚举序列中指定数目的帧数据元素。

## <a name="syntax"></a>语法

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>参数
 celt

中枚举序列中要跳过的帧数据元素的数目。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，如果没有其他要跳过的记录，将返回 `S_FALSE`。

## <a name="see-also"></a>请参阅
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)