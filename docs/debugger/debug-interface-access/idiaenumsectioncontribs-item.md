---
title: IDiaEnumSectionContribs::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Item method
ms.assetid: 63a28f23-0ca0-44a7-b11b-ca0206d642a0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d021b5016bd0e0039f2bf175102dc44f04dabaab
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744298"
---
# <a name="idiaenumsectioncontribsitem"></a>IDiaEnumSectionContribs::Item
通过索引检索节基值。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   DWORD                index,
   IDiaSectionContrib** section
);
```

#### <a name="parameters"></a>参数
 索引

中要检索的[IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)对象的索引。 索引的范围为0到 `count`-1，其中 `count` 由[IDiaEnumSectionContribs：： get_Count](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-count.md)方法返回。

 section

弄返回一个[IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)对象，该对象表示所需的节内容。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSectionContribs::get_Count](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-count.md)
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)