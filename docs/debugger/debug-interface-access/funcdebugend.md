---
title: FuncDebugEnd |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- FuncDebugEnd symbol
- debugging [DIA SDK], end point
ms.assetid: 68f84fff-7cd3-4636-b929-7063a45009f8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1069d1a5f565d55fdb51d398087bd965933b6845
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62554637"
---
# <a name="funcdebugend"></a>FuncDebugEnd
如果函数具有一个定义的点处的调试是，最终，由具有的符号标识起始点的调试`SymTagFuncDebugEnd`标记。

## <a name="properties"></a>属性
 下表显示适用于此符号类型的属性。

|属性|数据类型|描述|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|偏移量部分的位置;有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|`DWORD`|位置; 部分一部分有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_customCallingConvention](../../debugger/debug-interface-access/idiasymbol-get-customcallingconvention.md)|`BOOL`|`TRUE` 如果该函数使用自定义调用约定 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_farReturn](../../debugger/debug-interface-access/idiasymbol-get-farreturn.md)|`BOOL`|`TRUE` 如果函数执行得返回了 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_interruptReturn](../../debugger/debug-interface-access/idiasymbol-get-interruptreturn.md)|`BOOL`|`TRUE` 如果函数包含从中断 （仅在 DIA SDK V8.0 或更高版本） 返回。|
|[IDiaSymbol::get_isStatic](../../debugger/debug-interface-access/idiasymbol-get-isstatic.md)|`BOOL`|`TRUE` 如果该函数是静态的 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|将封闭函数的符号。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|`DWORD`|终结点具有静态位置;有关详细信息，请参阅[符号位置](../../debugger/debug-interface-access/symbol-locations.md)。|
|[IDiaSymbol::get_noInline](../../debugger/debug-interface-access/idiasymbol-get-noinline.md)|`BOOL`|`TRUE` 如果该函数使用指定[noinline](/cpp/cpp/noinline)属性 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_noReturn](../../debugger/debug-interface-access/idiasymbol-get-noreturn.md)|`BOOL`|`TRUE` 如果该函数使用指定[noreturn](/cpp/cpp/noreturn)属性 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_notReached](../../debugger/debug-interface-access/idiasymbol-get-notreached.md)|`BOOL`|`TRUE` 如果 （仅在 DIA SDK V8.0 或更高版本），永远不会调用的函数。|
|[IDiaSymbol::get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md)|`LONG`|在内存中; 符号的偏移量有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)， `LocIsRegRel`。|
|[IDiaSymbol::get_optimizedCodeDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-optimizedcodedebuginfo.md)|`BOOL`|`TRUE` 如果函数具有为优化代码 （仅在 DIA SDK V8.0 或更高版本） 的调试信息。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|其模块中此函数的末尾的相对位置。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagFuncDebugEnd`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|`ULONGLONG`|此函数可执行映像中的位置。|

## <a name="see-also"></a>请参阅
- [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)
- [符号位置](../../debugger/debug-interface-access/symbol-locations.md)