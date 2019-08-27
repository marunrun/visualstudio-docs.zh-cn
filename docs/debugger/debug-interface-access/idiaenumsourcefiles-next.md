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
ms.openlocfilehash: 29424c2b12884cae7f803a46e15f7183d9690d96
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829623"
---
# <a name="idiaenumsourcefilesnext"></a>IDiaEnumSourceFiles::Next
检索指定的数目的枚举序列中的源文件。

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

[in]要检索的枚举器中的源文件数。

 rgelt

[out]数组，它是在用来填充[IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)对象表示所需的源文件。

 pceltFetched

[out]返回在提取枚举器中的源文件数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果没有更多的源文件。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)
- [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)