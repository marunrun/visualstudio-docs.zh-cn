---
title: IDiaSession::findSymbolByRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findSymbolByRVA method
ms.assetid: 14fb2903-b771-44d6-b0a8-44e0097c58ce
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bf6a32284588163aae57d03ec67c69a9f64663b0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839220"
---
# <a name="idiasessionfindsymbolbyrva"></a>IDiaSession::findSymbolByRVA
检索包含，或与指定的相对虚拟地址 (RVA) 最接近的指定的符号类型。

## <a name="syntax"></a>语法

```C++
HRESULT findSymbolByRVA ( 
   DWORD        rva,
   SymTagEnum   symtag,
   IDiaSymbol** ppSymbol
);
```

#### <a name="parameters"></a>参数
 `rva`

[in]指定 RVA。

 `symtag`

[in]要查找的符号类型。 值取自[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)枚举。

 `ppSymbol`

[out]返回[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)检索表示该符号的对象。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="example"></a>示例

```C++
IDiaSymbol* pFunc;
pSession->findSymbolByRVA( rva, SymTagFunction, &pFunc );
```

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)