---
title: IDiaSession::findInlineeLinesByLinenum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: cf32ae7c-a0c8-4800-bc8f-d64fdd15fb06
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 493e1a2f6df57019183f36daf246ef69e8f1a4d6
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63402615"
---
# <a name="idiasessionfindinlineelinesbylinenum"></a>IDiaSession::findInlineeLinesByLinenum
检索一个枚举，允许客户端进行循环访问，将内联，直接或间接指定的源文件和行号中的所有函数的行号信息。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineeLinesByVA ( 
   IDiaSymbol*           compiland,
   IDiaSourceFile*       file,
   DWORD                 linenum,
   DWORD                 column,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
 `compiland`

[in][IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，表示要在其中搜索的行号编译单位。 此参数不能为 `NULL`。

 `file`

[in][IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)对象，表示要在其中搜索源文件。 此参数不能为 `NULL`。

 `linenum`

[in]指定基于 1 的行号。

> [!NOTE]
> 您不能使用零指定所有行 (使用[idiasession:: Findlines](../../debugger/debug-interface-access/idiasession-findlines.md)方法来查找所有行)。

 `column`

[in]指定的列号。 使用零来指定所有列。 列是行的字节的偏移量。

 `ppResult`

[out]返回[IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)对象，其中包含检索到的行号的列表。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)