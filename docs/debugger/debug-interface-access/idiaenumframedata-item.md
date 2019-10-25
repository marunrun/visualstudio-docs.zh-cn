---
title: IDiaEnumFrameData::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::Item method
ms.assetid: 2761a72d-1868-4f5b-a32e-c2a1d9358c91
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9c15f395e7f4aa576c5f69b0f1c61f37ca808fb6
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744612"
---
# <a name="idiaenumframedataitem"></a>IDiaEnumFrameData::Item
通过索引检索帧数据元素。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   DWORD           index,
   IDiaFrameData** section
);
```

#### <a name="parameters"></a>参数
 索引

中要检索的[IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)对象的索引。 索引的范围为0到 `count`-1，其中 `count` 由[IDiaEnumFrameData：： get_Count](../../debugger/debug-interface-access/idiaenumframedata-get-count.md)方法返回。

 section

弄返回表示所需帧数据元素的[IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)对象。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)