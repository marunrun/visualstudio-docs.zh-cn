---
title: IDiaEnumLineNumbers：： Next |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers::Next method
ms.assetid: 363d5b40-1316-4ab8-836f-63637f619e0a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 07402ef7028ecfb7bb5b2c6e33ae06bc98ffe709
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744394"
---
# <a name="idiaenumlinenumbersnext"></a>IDiaEnumLineNumbers::Next
检索枚举序列中指定数目的行号。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
   ULONG            celt,
   IDiaLineNumber** rgelt,
   ULONG*           pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

中要检索的枚举器中的行号数目。

 rgelt

弄返回[IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)对象的数组，这些对象表示所需的行号。

 pceltFetched

弄返回提取的枚举器中的行号数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多的行号，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
- [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)