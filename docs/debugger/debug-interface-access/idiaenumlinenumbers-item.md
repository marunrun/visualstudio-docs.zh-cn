---
title: IDiaEnumLineNumbers::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers::Item method
ms.assetid: 08efbeaf-22f7-49e9-96a8-bb906dfe4fd8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9bba71efce68864b8737011ab7dda5cb8da3267c
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744403"
---
# <a name="idiaenumlinenumbersitem"></a>IDiaEnumLineNumbers::Item
通过索引检索行号。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   DWORD            index,
   IDiaLineNumber** lineNumber
);
```

#### <a name="parameters"></a>参数
 索引

中要检索的[IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)对象的索引。 索引的范围为0到 `count`-1，其中 `count` 由[IDiaEnumLineNumbers：： get_Count](../../debugger/debug-interface-access/idiaenumlinenumbers-get-count.md)方法返回。

 lineNumber

弄返回一个[IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)对象，该对象表示所需的行号。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)