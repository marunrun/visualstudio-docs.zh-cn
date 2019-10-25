---
title: IDiaSession：： findSymbolByToken |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findSymbolByToken method
ms.assetid: 3c92149c-6eef-454f-86be-66e89557b9e6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 098d84d6c7c79fee5fea5e5b2b36136bf7b55b26
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742028"
---
# <a name="idiasessionfindsymbolbytoken"></a>IDiaSession::findSymbolByToken
检索包含指定的元数据标记的符号。

## <a name="syntax"></a>语法

```C++
HRESULT findSymbolByToken ( 
   ULONG        token,
   SymTagEnum   symtag,
   IDiaSymbol** ppSymbol
);
```

#### <a name="parameters"></a>参数
 `token`

中指定令牌。

 `symtag`

中要查找的符号类型。 值取自[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)枚举。

 `ppSymbol`

弄返回一个[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，该对象表示检索到的符号。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="example"></a>示例

```C++
IDiaSymbol* pFunc;
pSession->findSymbolByToken( token, SymTagFunction, &pFunc );
```

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)