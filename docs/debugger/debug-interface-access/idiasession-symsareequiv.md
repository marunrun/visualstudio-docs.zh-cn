---
title: IDiaSession::symsAreEquiv | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::symsAreEquiv method
ms.assetid: 9941d520-e203-46c0-83c3-b3a967f4fc59
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 61cfc582f11670af8c956c3334681284ce5172a6
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741869"
---
# <a name="idiasessionsymsareequiv"></a>IDiaSession::symsAreEquiv
检查两个符号是否等效。

## <a name="syntax"></a>语法

```C++
HRESULT symsAreEquiv ( 
   IDiaSymbol* symbolA,
   IDiaSymbol* symbolB
);
```

#### <a name="parameters"></a>参数
 `symbolA`

中在比较中使用的第一个[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象。

 `symbolB`

中比较中使用的第二个 `IDiaSymbol` 对象。

## <a name="return-value"></a>返回值
 如果符号等效，则返回 `S_OK`;否则，将返回 `S_FALSE`，则符号不等效。 否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)