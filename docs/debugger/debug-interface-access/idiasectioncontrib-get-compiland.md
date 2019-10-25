---
title: IDiaSectionContrib：： get_compiland |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_compiland method
ms.assetid: c0496f6f-f8f2-435f-8674-6c32db6c5934
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d9a398d7cc0ff8efc9dacc726205cd0d8fa02473
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742706"
---
# <a name="idiasectioncontribget_compiland"></a>IDiaSectionContrib::get_compiland
检索对此部分提供的编译单位符号的引用。

## <a name="syntax"></a>语法

```C++
HRESULT get_compiland ( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回表示提供此部分的编译单位的[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果此属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)