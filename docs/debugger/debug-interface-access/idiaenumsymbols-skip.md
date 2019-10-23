---
title: IDiaEnumSymbols：： Skip |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbols::Skip method
ms.assetid: e601fbc9-b10b-41c7-8180-959e57efabe8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9252826470decd3cddfabdcc2a00e22037d5de5c
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743912"
---
# <a name="idiaenumsymbolsskip"></a>IDiaEnumSymbols::Skip
跳过枚举序列中指定数目的符号。

## <a name="syntax"></a>语法

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>参数
 celt

中要跳过的枚举序列中的符号数。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，如果没有其他要跳过的符号，将返回 `S_FALSE`。

## <a name="see-also"></a>请参阅
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)