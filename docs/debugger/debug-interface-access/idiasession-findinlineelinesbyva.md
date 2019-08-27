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
ms.openlocfilehash: 58f572fcce0b490fad8f94f1e3e3d941e8568211
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827718"
---
# <a name="idiasessionfindinlineelinesbyva"></a>IDiaSession::findInlineeLinesByVA
检索一个枚举，它允许客户端可以循环访问的所有函数的内联，直接或间接地，由指定的父符号的行号信息且包含在指定的虚拟地址 (VA)。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineeLinesByVA ( 
   IDiaSymbol*           parent,   ULONGLONG             va,   DWORD                 length,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
 `parent`

[in]`IDiaSymbol`表示父对象。

 `va`

[in]指定的地址作为弗吉尼亚

 `length`

[in]中的字节数，以覆盖与此查询指定地址范围。

 `ppResult`

[out]保存`IDiaEnumLineNumbers`对象，其中包含检索到的行号的列表。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)