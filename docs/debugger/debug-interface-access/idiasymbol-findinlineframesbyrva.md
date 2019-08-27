---
title: IDiaSymbol::findInlineFramesByRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: e7a6d9cb-2726-4ac7-9f38-415ad215bf9c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d43863f44ec80dce283b1746be12f7a6f47cfe4f
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62838979"
---
# <a name="idiasymbolfindinlineframesbyrva"></a>IDiaSymbol::findInlineFramesByRVA
检索一个枚举，允许客户端用于循环访问所有指定的相对虚拟地址 (RVA) 上的内联框架。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineFramesByRVA (    DWORD             rva,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>参数
 `rva`

[in]RVA 作为指定的地址。

 `ppResult`

[out]保存`IDiaEnumSymbols`对象，其中包含检索到的框架的列表。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)