---
title: IDiaSymbol::findInlineFramesByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 54295d3e-bbb6-4c10-ab9d-adcfc22b1f71
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f2ec0280f7eab6d5dd44c4577cfde2cd3846e5fd
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741142"
---
# <a name="idiasymbolfindinlineframesbyva"></a>IDiaSymbol::findInlineFramesByVA
检索一个枚举，该枚举允许客户端循环访问指定虚拟地址（VA）上的所有内联帧。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineFramesByVA ( 
   ULONGLONG         va,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>参数
 `va`

中指定地址作为 VA。

 `ppResult`

弄保存一个 `IDiaEnumSymbols` 对象，该对象包含所检索到的帧的列表。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)