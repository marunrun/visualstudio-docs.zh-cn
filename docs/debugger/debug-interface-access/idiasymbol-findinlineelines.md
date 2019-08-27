---
title: IDiaSymbol::findInlineeLines |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 56ba4bc0-8f96-47c2-8b18-332b4e7c2d91
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c2f5f38205770b7b7574a37b700b3c9b23b4fe90
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62832432"
---
# <a name="idiasymbolfindinlineelines"></a>IDiaSymbol::findInlineeLines
检索一个枚举，允许客户端来循环访问的所有函数的内联，直接或间接地，此符号中的行号信息。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineeLines ( 
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
 `ppResult`

[out]保存`IDiaEnumLineNumbers`对象，其中包含检索到的行号的列表。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaSession::findInlineeLines](../../debugger/debug-interface-access/idiasession-findinlineelines.md)