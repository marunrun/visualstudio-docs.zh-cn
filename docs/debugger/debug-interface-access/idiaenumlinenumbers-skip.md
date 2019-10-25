---
title: IDiaEnumLineNumbers：： Skip |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers::Skip method
ms.assetid: d182c269-8c76-4d8b-8275-c6807c5ae4e1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 58b959db58688fd13c3539f720315971e774a96d
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744364"
---
# <a name="idiaenumlinenumbersskip"></a>IDiaEnumLineNumbers::Skip
跳过枚举序列中指定数目的行号。

## <a name="syntax"></a>语法

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>参数
 celt

中枚举序列中要跳过的行号的数目。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，如果没有更多的行号要跳过，则返回 `S_FALSE`。

## <a name="see-also"></a>请参阅
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)