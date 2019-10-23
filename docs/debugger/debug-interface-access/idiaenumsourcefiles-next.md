---
title: IDiaEnumSourceFiles::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSourceFiles::Next method
ms.assetid: 83bf6317-ff39-4c5c-8987-cba34e7a6983
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 526c857acbe1283e16312355c181c56c67e19883
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744080"
---
# <a name="idiaenumsourcefilesnext"></a>IDiaEnumSourceFiles::Next
检索枚举序列中指定数目的源文件。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
   ULONG            celt,
   IDiaSourceFile** rgelt,
   ULONG*           pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

中要检索的枚举器中的源文件数。

 rgelt

弄一个数组，它将用表示所需源文件的[IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)对象进行填充。

 pceltFetched

弄返回提取的枚举器中的源文件数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多的源文件，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)
- [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)