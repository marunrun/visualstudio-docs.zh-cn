---
title: IDiaSession::findLinesByAddr | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findLinesByAddr method
ms.assetid: 640403c0-14cf-403c-ad19-38b3bdc28ca8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 328589df0e662ca27db634017005344d44491275
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742108"
---
# <a name="idiasessionfindlinesbyaddr"></a>IDiaSession::findLinesByAddr
检索指定编译单位中包含指定地址的行。

## <a name="syntax"></a>语法

```C++
HRESULT findLinesByAddr (
    DWORD                 seg,
    DWORD                 offset,
    DWORD                 length,
    IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
`seg`

中指定特定地址的部分组件。

`offset`

中指定特定地址的偏移量部分。

`length`

中指定包含此查询的地址范围的字节数。

`ppResult`

弄返回一个[IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)对象，该对象包含涵盖指定地址范围的所有行号的列表。

## <a name="return-value"></a>返回值
如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="example"></a>示例
此示例演示一个函数，该函数使用函数的地址和长度获取函数中包含的所有行号。

```C++
IDiaEnumLineNumbers* GetLineNumbersByAddr(IDiaSymbol *pFunc,
                                          IDiaSession *pSession)
{
    IDiaEnumLineNumbers* pEnum = NULL;
    DWORD                seg;
    DWORD                offset;
    ULONGLONG            length;

    if (pFunc->get_addressSection ( &seg ) == S_OK &&
        pFunc->get_addressOffset ( &offset ) == S_OK)
    {
        pFunc->get_length ( &length );
        pSession->findLinesByAddr( seg, offset, static_cast<DWORD>( length ), &pEnum );
    }
    return(pEnum);
}
```

## <a name="see-also"></a>请参阅
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSession::findLinesByVA](../../debugger/debug-interface-access/idiasession-findlinesbyva.md)
