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
ms.openlocfilehash: 3af9915498182338a1b0ffa463f19d9867e76402
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742045"
---
# <a name="idiasessionfindsymbolbyrva"></a>IDiaSession::findSymbolByRVA
检索指定的符号类型，该类型包含指定的相对虚拟地址（RVA），或该类型最接近指定的相对虚拟地址（RVA）。

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

中指定 RVA。

 `symtag`

中要查找的符号类型。 值取自[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)枚举。

 `ppSymbol`

弄返回一个[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，该对象表示检索到的符号。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="example"></a>示例

```C++
IDiaSymbol* pFunc;
pSession->findSymbolByRVA( rva, SymTagFunction, &pFunc );
```

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)