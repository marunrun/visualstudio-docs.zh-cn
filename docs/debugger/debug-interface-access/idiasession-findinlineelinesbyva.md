---
title: IDiaSession::findInlineeLinesByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: dffe6594-e0d1-4ed5-aeea-8773f88d82a6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 24807114cbb28c4112f538b8aa88b26bf5491fef
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742194"
---
# <a name="idiasessionfindinlineelinesbyva"></a>IDiaSession::findInlineeLinesByVA
检索一个枚举，该枚举允许客户端通过指定的父符号直接或间接地循环访问所有函数的行号信息，并将其包含在指定的虚拟地址（VA）中。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineeLinesByVA ( 
   IDiaSymbol*           parent,   ULONGLONG             va,   DWORD                 length,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
 `parent`

中表示父级的 `IDiaSymbol` 对象。

 `va`

中指定地址作为 VA。

 `length`

中指定要用于此查询的地址范围（以字节数为单位）。

 `ppResult`

弄保存一个包含所检索的行号列表的 `IDiaEnumLineNumbers` 对象。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)