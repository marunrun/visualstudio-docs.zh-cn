---
title: 标签 （调试接口访问 SDK） |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- locations, in program code
- Label symbol
ms.assetid: 8cef7620-5bc8-4500-8bd0-e9e638bccb24
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b445c5f8be55d5290feb1318a3b937980a3e5c06
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62834336"
---
# <a name="label-debug-interface-access-sdk"></a>标签（调试接口访问 SDK）
在程序代码中的位置由`SymTagLabel`符号。

## <a name="properties"></a>属性
 下表显示适用于此符号类型的属性。

|属性|数据类型|描述|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|偏移量部分的位置;有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|`DWORD`|位置; 部分一部分有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_customCallingConvention](../../debugger/debug-interface-access/idiasymbol-get-customcallingconvention.md)|`BOOL`|`TRUE` 如果标签使用自定义调用约定。|
|[IDiaSymbol::get_farReturn](../../debugger/debug-interface-access/idiasymbol-get-farreturn.md)|`BOOL`|`TRUE` 如果标签执行得返回。|
|[IDiaSymbol::get_interruptReturn](../../debugger/debug-interface-access/idiasymbol-get-interruptreturn.md)|`BOOL`|`TRUE` 如果标签包含从中断的返回。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|封闭的编译单位、 块或函数的符号。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|`DWORD`|标签具有静态位置;有关详细信息，请参阅[符号位置](../../debugger/debug-interface-access/symbol-locations.md)枚举。|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|标签的名称。|
|[IDiaSymbol::get_noInline](../../debugger/debug-interface-access/idiasymbol-get-noinline.md)|`BOOL`|`TRUE` 如果使用指定的标签[noinline](/cpp/cpp/noinline)属性。|
|[IDiaSymbol::get_noReturn](../../debugger/debug-interface-access/idiasymbol-get-noreturn.md)|`BOOL`|`TRUE` 如果使用指定的标签[noreturn](/cpp/cpp/noreturn)属性。|
|[IDiaSymbol::get_notReached](../../debugger/debug-interface-access/idiasymbol-get-notreached.md)|`BOOL`|`TRUE` 如果永远不会调用该标签。|
|[IDiaSymbol::get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md)|`LONG`|在内存中; 符号的偏移量有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)， `LocIsRegRel`。|
|[IDiaSymbol::get_optimizedCodeDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-optimizedcodedebuginfo.md)|`BOOL`|`TRUE` 如果代码具有优化的代码的调试信息。|
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|其模块内的此标签的相对位置。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagFuncDebugLabel`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|`ULONGLONG`|可执行映像中的此标签的位置。|

## <a name="see-also"></a>请参阅
- [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)
- [符号位置](../../debugger/debug-interface-access/symbol-locations.md)