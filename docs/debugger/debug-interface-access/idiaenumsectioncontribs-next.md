---
title: IDiaEnumSectionContribs::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Next method
ms.assetid: a6bb2adb-ee6d-4f3c-ab5b-e89361c8880e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 61d99b0c881abdb8974e94352911ae3234c440c1
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744278"
---
# <a name="idiaenumsectioncontribsnext"></a>IDiaEnumSectionContribs::Next
检索枚举序列中指定数目的节内容。

## <a name="syntax"></a>语法

```C++
HRESULT Next( 
   ULONG                celt,
   IDiaSectionContrib** rgelt,
   ULONG*               pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

中要检索的枚举器中的部分发布数。

 rgelt

弄一个数组，该数组将用表示所需的节发布的[IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)对象进行填充。

 pceltFetched

弄返回提取的枚举器中的部分发布数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多的节基值，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)