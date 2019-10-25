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
ms.openlocfilehash: fe238f3bc66d6a7c5978c5d7cbebcd185fcd43d2
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742215"
---
# <a name="idiasessionfindinlineelinesbylinenum"></a>IDiaSession::findInlineeLinesByLinenum
检索一个枚举，该枚举允许客户端循环访问指定源文件和行号内直接或间接内联的所有函数的行号信息。

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

中表示要在其中搜索行号的编译单位的[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象。 此参数不能为 `NULL`。

 `file`

中一个[IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)对象，该对象表示要在其中进行搜索的源文件。 此参数不能为 `NULL`。

 `linenum`

中指定一个从1开始的行号。

> [!NOTE]
> 不能使用零来指定所有行（使用[IDiaSession：： findLines](../../debugger/debug-interface-access/idiasession-findlines.md)方法查找所有行）。

 `column`

中指定列号。 使用零来指定所有列。 列是行中的字节偏移量。

 `ppResult`

弄返回一个[IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)对象，该对象包含检索到的行号的列表。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)