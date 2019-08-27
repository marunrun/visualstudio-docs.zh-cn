---
title: 函数 （调试接口访问 SDK） |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Function symbol
ms.assetid: 458dc91c-b78b-4427-84f4-615d89e26760
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4d1e0af87618955c492bef68be45c8c623f41218
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62554513"
---
# <a name="function-debug-interface-access-sdk"></a>函数（调试接口访问 SDK）
每个函数由`SymTagFunction`符号。

## <a name="properties"></a>属性
 下表显示适用于此符号类型的属性。

|属性|`Data type`|描述|
|--------------|-----------------|-----------------|
|[IDiaSymbol::get_access](../../debugger/debug-interface-access/idiasymbol-get-access.md)|`DWORD`|值之一[CV_access_e 枚举](../../debugger/debug-interface-access/cv-access-e.md)，如果该函数是成员函数。|
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|偏移量部分的位置;有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|`DWORD`|位置; 部分一部分有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)|`IDiaSymbol*`|对于类，如果该函数是成员函数的符号。|
|[IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)|`DWORD`|类父符号的 ID。|
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|`BOOL`|`TRUE` 如果该函数标记为常量。|
|[IDiaSymbol::get_customCallingConvention](../../debugger/debug-interface-access/idiasymbol-get-customcallingconvention.md)|`BOOL`|`TRUE` 如果该函数使用自定义调用约定 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_farReturn](../../debugger/debug-interface-access/idiasymbol-get-farreturn.md)|`BOOL`|`TRUE` 如果函数不执行得返回 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_hasAlloca](../../debugger/debug-interface-access/idiasymbol-get-hasalloca.md)|`BOOL`|`TRUE` 如果该函数使用分配的内存函数 (仅 uinnder DIA SDK V8.0 或更高版本)。|
|[IDiaSymbol::get_hasEH](../../debugger/debug-interface-access/idiasymbol-get-haseh.md)|`BOOL`|`TRUE` 如果该函数包含C++-样式异常处理 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_hasEHa](../../debugger/debug-interface-access/idiasymbol-get-haseha.md)|`BOOL`|`TRUE` 如果该函数包含异步异常处理 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_hasInlAsm](../../debugger/debug-interface-access/idiasymbol-get-hasinlasm.md)|`BOOL`|`TRUE` 如果该函数包含内联程序集 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_hasLongJump](../../debugger/debug-interface-access/idiasymbol-get-haslongjump.md)|`BOOL`|`TRUE` 如果该函数包含[longjmp](/cpp/c-runtime-library/reference/longjmp)调用 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_hasSecurityChecks](../../debugger/debug-interface-access/idiasymbol-get-hassecuritychecks.md)|`BOOL`|`TRUE` 如果该函数包含安全检查 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_hasSEH](../../debugger/debug-interface-access/idiasymbol-get-hasseh.md)|`BOOL`|`TRUE` 如果该函数包含 Win32 样式结构化异常处理 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_hasSetJump](../../debugger/debug-interface-access/idiasymbol-get-hassetjump.md)|`BOOL`|`TRUE` 如果该函数包含[setjmp](/cpp/c-runtime-library/reference/setjmp)调用 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_interruptReturn](../../debugger/debug-interface-access/idiasymbol-get-interruptreturn.md)|`BOOL`|`TRUE` 如果函数具有从中断 （仅在 DIA SDK V8.0 或更高版本） 返回。|
|[IDiaSymbol::get_intro](../../debugger/debug-interface-access/idiasymbol-get-intro.md)|`BOOL`|`TRUE` 如果函数是虚拟的简介。|
|[IDiaSymbol::get_InlSpec](../../debugger/debug-interface-access/idiasymbol-get-inlspec.md)|`BOOL`|`TRUE` 如果该函数已标记有之一[inline、 __inline、 \__forceinline](/cpp/cpp/inline-functions-cpp)属性。|
|[IDiaSymbol::get_isNaked](../../debugger/debug-interface-access/idiasymbol-get-isnaked.md)|`BOOL`|`TRUE` 如果该函数将标有[裸](/cpp/cpp/naked-cpp)属性 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_isStatic](../../debugger/debug-interface-access/idiasymbol-get-isstatic.md)|`BOOL`|`TRUE` 如果该函数是静态的 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|`ULONGLONG`|函数代码中，从位置开始的字节数。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|将封闭的编译单位符号。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|`DWORD`|函数可以具有静态或元数据的位置;有关详细信息，请参阅[符号位置](../../debugger/debug-interface-access/symbol-locations.md)。|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|函数的名称。|
|[IDiaSymbol::get_noInline](../../debugger/debug-interface-access/idiasymbol-get-noinline.md)|`BOOL`|`TRUE` 如果该函数不是内联函数 (仅 n DIA SDK V8.0 或更高版本)。|
|[IDiaSymbol::get_notReached](../../debugger/debug-interface-access/idiasymbol-get-notreached.md)|`BOOL`|`TRUE` 如果该函数不是可访问 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_noReturn](../../debugger/debug-interface-access/idiasymbol-get-noreturn.md)|`BOOL`|`TRUE` 如果该函数不返回值 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_noStackOrdering](../../debugger/debug-interface-access/idiasymbol-get-nostackordering.md)|`BOOL`|`TRUE` 如果函数已编译带缓冲区安全性检查但无法执行没有堆栈一定的顺序。|
|[IDiaSymbol::get_optimizedCodeDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-optimizedcodedebuginfo.md)|`BOOL`|`TRUE` 如果代码具有为优化代码 （仅在 DIA SDK V8.0 或更高版本） 的调试信息。|
|[IDiaSymbol::get_pure](../../debugger/debug-interface-access/idiasymbol-get-pure.md)|`BOOL`|`TRUE` 如果函数是纯虚拟。|
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|此函数在其模块内的相对位置。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagFunction`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|
|[IDiaSymbol::get_token](../../debugger/debug-interface-access/idiasymbol-get-token.md)|`DWORD`|该函数的元数据标记。|
|[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)|`IDiaSymbol*`|函数签名的符号。|
|[IDiaSymbol::get_typeId](../../debugger/debug-interface-access/idiasymbol-get-typeid.md)|`DWORD`|类型符号的 ID。|
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|`BOOL`|`TRUE` 如果函数未对齐。|
|[IDiaSymbol::get_undecoratedName](../../debugger/debug-interface-access/idiasymbol-get-undecoratedname.md)|`BSTR`|未修饰的形式的函数名称 （仅在 DIA SDK v8.0 或更高版本）|
|[IDiaSymbol::get_undecoratedNameEx](../../debugger/debug-interface-access/idiasymbol-get-undecoratednameex.md)|`BSTR`|部分或全部函数名称 （仅在 DIA SDK v8.0 或更高版本） 的未修饰形式。|
|[IDiaSymbol::get_virtual](../../debugger/debug-interface-access/idiasymbol-get-virtual.md)|`BOOL`|`TRUE` 如果虚拟函数。|
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|`ULONGLONG`|此函数可执行映像中的位置。|
|[IDiaSymbol::get_virtualBaseOffset](../../debugger/debug-interface-access/idiasymbol-get-virtualbaseoffset.md)|`DWORD`|如果虚拟函数，然后在虚函数表中的偏移量。|
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|`BOOL`|`TRUE` 如果该函数标记为易失性。|

## <a name="see-also"></a>请参阅
- [CV_access_e 枚举](../../debugger/debug-interface-access/cv-access-e.md)
- [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)
- [符号位置](../../debugger/debug-interface-access/symbol-locations.md)