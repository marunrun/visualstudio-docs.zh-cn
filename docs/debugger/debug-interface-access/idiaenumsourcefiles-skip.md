---
title: IDiaEnumSourceFiles::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSourceFiles::Skip method
ms.assetid: 4821e6dd-d33f-403d-857d-e3ae81e4a9e3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d7aef3ea724bbb50f0342032a62e0044a1f0eb30
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744056"
---
# <a name="idiaenumsourcefilesskip"></a>IDiaEnumSourceFiles::Skip
跳过枚举序列中指定数目的源文件。

## <a name="syntax"></a>语法

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>参数
 celt

中要跳过的枚举序列中的源文件数。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，如果没有更多要跳过的源文件，则返回 `S_FALSE`。

## <a name="see-also"></a>请参阅
- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)