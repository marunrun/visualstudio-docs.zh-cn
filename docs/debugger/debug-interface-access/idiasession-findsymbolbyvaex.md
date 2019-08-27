---
title: 'Idiasession:: Findsymbolbyvaex |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findSymbolByVAEx method
ms.assetid: 11c685f6-cda2-4474-a432-214ecaae4ffa
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 16b62c5efb520e90606d6311b60a839404359720
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832358"
---
# <a name="idiasessionfindsymbolbyvaex"></a>IDiaSession::findSymbolByVAEx
检索包含，或与指定的虚拟地址 (VA) 和偏移量最接近的指定的符号类型。

## <a name="syntax"></a>语法

```C++
HRESULT findSymbolByVAEx ( 
   ULONGLONG    va,
   SymTagEnum   symtag,
   IDiaSymbol** ppSymbol,
   LONG*        displacement
);
```

#### <a name="parameters"></a>参数
 `va`

[in]指定弗吉尼亚

 `symtag`

[in]要查找的符号类型。 值取自[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)枚举。

 `ppSymbol`

[out]返回[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)检索表示该符号的对象。

 `displacement`

[out]返回一个值，指定与给定的虚拟地址的偏移量`va`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="example"></a>示例

```C++
IDiaSymbol* pFunc;
LONG disp = 0;
pSession->findSymbolByVAEx( va, SymTagFunction, &pFunc, &disp );
```

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)