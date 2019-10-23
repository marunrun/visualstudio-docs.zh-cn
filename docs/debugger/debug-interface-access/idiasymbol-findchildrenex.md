---
title: IDiaSymbol：： findChildrenEx |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::findChildrenEx
ms.assetid: 6e045045-da8c-4338-9423-81a1ca20c405
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 26fdced012baada390cdd0a112856b592d3c923e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741269"
---
# <a name="idiasymbolfindchildrenex"></a>IDiaSymbol::findChildrenEx
检索符号的子元素。 如果在中对程序进行了优化，则返回的本地符号包含实时范围信息。

## <a name="syntax"></a>语法

```C++
HRESULT findChildrenEx ( 
   enum SymTagEnum   symtag,
   LPCOLESTR         name,
   DWORD             compareFlags,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>参数
 `symtag`

中指定要检索的子级的符号标记，如[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)中所定义。 设置为要检索的所有子级 `SymTagNull`。

 `name`

中指定要检索的子项的名称。 设置为要检索的所有子级 `NULL`。

 `compareFlags`

中指定要应用于名称匹配的比较选项。 [NameSearchOptions 枚举](../../debugger/debug-interface-access/namesearchoptions.md)枚举中的值可以单独使用，也可以组合使用。

 `ppResult`

弄返回一个[IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)对象，该对象包含所检索到的子符号的列表。

## <a name="return-value"></a>返回值
 如果找到至少一个符号子级，则返回 `S_OK`; 如果未找到任何子级，则返回 `S_FALSE`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 此方法是[IDiaSymbol：： findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)的扩展版本。

## <a name="requirements"></a>要求
 标头： Dia2

 库： diaguids

 DLL： msdia100

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [NameSearchOptions 枚举](../../debugger/debug-interface-access/namesearchoptions.md)