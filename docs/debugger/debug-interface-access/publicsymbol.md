---
title: PublicSymbol |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- data symbols [C++]
- PublicSymbol symbol
- global functions [C++], as public symbols
ms.assetid: f8d33007-302d-4549-9dad-47fb33ea60b7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c2c042d75ad74cc42d94596d60008dc43704e612
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62854883"
---
# <a name="publicsymbol"></a>PublicSymbol
当创建.exe 文件时，提供每个公共符号 （@ 最小值、 每个全局函数和数据符号）`SymTagPublicSymbol`标记。

## <a name="properties"></a>属性
 下表显示适用于此符号类型的属性。

|属性|数据类型|描述|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|偏移量部分的位置;有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|`DWORD`|位置; 部分一部分有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_code](../../debugger/debug-interface-access/idiasymbol-get-code.md)|`BOOL`|`TRUE` 如果符号的位置是在代码中。|
|[IDiaSymbol::get_function](../../debugger/debug-interface-access/idiasymbol-get-function.md)|`BOOL`|`TRUE` 如果符号为一个函数。|
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|`ULONGLONG`|此符号以字节为单位的长度。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|全局作用域的的符号。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|`DWORD`|公共符号具有静态位置;有关详细信息，请参阅[符号位置](../../debugger/debug-interface-access/symbol-locations.md)。|
|[IDiaSymbol::get_managed](../../debugger/debug-interface-access/idiasymbol-get-managed.md)|`BOOL`|`TRUE` 如果符号的位置是在托管代码中。|
|[IDiaSymbol::get_msil](../../debugger/debug-interface-access/idiasymbol-get-msil.md)|`BOOL`|`TRUE` 如果符号的位置是在 Microsoft 中间语言 (MSIL) 代码中。|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|完全修饰的符号名称。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|它的块中的符号的相对位置。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagPublicSymbol`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|
|[IDiaSymbol::get_undecoratedName](../../debugger/debug-interface-access/idiasymbol-get-undecoratedname.md)|`BSTR`|未修饰的符号名称。|
|[IDiaSymbol::get_undecoratedNameEx](../../debugger/debug-interface-access/idiasymbol-get-undecoratednameex.md)|`BSTR`|部分或全部未修饰的符号名称。|

## <a name="see-also"></a>请参阅
- [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)
- [符号位置](../../debugger/debug-interface-access/symbol-locations.md)