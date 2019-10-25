---
title: IDiaSession::symbolById | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::symbolById method
ms.assetid: 062e4b5a-9c4d-4703-88da-ec13102c2b66
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b0ffcb6c438150bff82f17a66c3347c300b17d72
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741879"
---
# <a name="idiasessionsymbolbyid"></a>IDiaSession::symbolById
按其唯一标识符检索符号。

## <a name="syntax"></a>语法

```C++
HRESULT symbolById (
    DWORD        id,
    IDiaSymbol** ppSymbol
);
```

#### <a name="parameters"></a>参数
`id`

中唯一标识符。

`ppSymbol`

弄返回一个[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，该对象表示检索到的符号。

## <a name="return-value"></a>返回值
如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
指定的标识符是 DIA SDK 在内部用来使所有符号都唯一的唯一值。

例如，可以使用此方法来检索表示另一个符号类型的符号（请参阅示例）。

## <a name="example"></a>示例
此示例检索表示另一个符号类型的[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 。 此示例演示如何使用会话中的 `symbolById` 方法。 更简单的方法是调用[IDiaSymbol：： get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)方法直接检索类型符号。

```C++
IDiaSymbol *GetSymbolType(IDiaSymbol *pSymbol, IDiaSession *pSession)
{
    IDiaSymbol *pTypeSymbol = NULL;
    if (pSymbol != NULL && pSession != NULL)
    {
        DWORD symbolTypeId;
        pSymbol->get_typeId(&symbolTypeId);
        pSession->symbolById(symbolTypeId, &pTypeSymbol);
    }
    return(pTypeSymbol);
}
```

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)
