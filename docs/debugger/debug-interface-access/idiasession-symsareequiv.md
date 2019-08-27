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
ms.openlocfilehash: 0253104cf29e86825fadc8c8bd18133e0d3cf593
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839070"
---
# <a name="idiasessionsymsareequiv"></a>IDiaSession::symsAreEquiv
检查以查看两个符号是否等效。

## <a name="syntax"></a>语法

```C++
HRESULT symsAreEquiv ( 
   IDiaSymbol* symbolA,
   IDiaSymbol* symbolB
);
```

#### <a name="parameters"></a>参数
 `symbolA`

[in]第一个[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)则比较中使用的对象。

 `symbolB`

[in]第二个`IDiaSymbol`则比较中使用的对象。

## <a name="return-value"></a>返回值
 如果符号为等效，返回`S_OK`; 否则为返回`S_FALSE`，符号不等效。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)