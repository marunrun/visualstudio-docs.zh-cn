---
title: 转换 （thunk) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- thunk properties [DIA SDK]
- thunk symbol
ms.assetid: 01abb95f-d89a-465c-a4eb-8e8509598c95
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 68e5542f3257ead72c13d454affbd0713325a7b4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62576364"
---
# <a name="thunk"></a>Thunk
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

每个`thunk`由`SymTagThunk`标记。  
  
## <a name="properties"></a>属性  
 下表显示适用于此符号类型的属性。  
  
|属性|数据类型|描述|  
|--------------|---------------|-----------------|  
|[IDiaSymbol::get_access](../../debugger/debug-interface-access/idiasymbol-get-access.md)|`DWORD`|访问修饰符属性之一[CV_access_e 枚举](../../debugger/debug-interface-access/cv-access-e.md)值 （仅在 DIA SDK V8.0 或更高版本）。|  
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|偏移量部分的位置;有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|  
|[IDiaSegment::get_addressSection](../../debugger/debug-interface-access/idiasegment-get-addresssection.md)|`DWORD`|位置; 部分一部分有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|  
|[IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)|`IDiaSymbol*`|封闭类父项，如果有 （仅在 DIA SDK V8.0 或更高版本）。|  
|[IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)|`DWORD`|封闭类父符号 （仅在 DIA SDK V8.0 或更高版本） 的 ID。|  
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|`BOOL`|如果转换 （thunk） 标记为常量 （仅在 DIA SDK V8.0 或更高版本），则为 TRUE。|  
|[IDiaSymbol::get_intro](../../debugger/debug-interface-access/idiasymbol-get-intro.md)|`BOOL`|如果转换 （thunk） 是虚函数 （仅在 DIA SDK V8.0 或更高版本） 的简介，则返回 TRUE|  
|[IDiaSymbol::get_isStatic](../../debugger/debug-interface-access/idiasymbol-get-isstatic.md)|`BOOL`|如果转换 （thunk） 被视为静态 （仅在 DIA SDK V8.0 或更高版本），则为 TRUE。|  
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|`ULONGLONG`|转换 （thunk） 中的代码的字节数。|  
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|封闭的编译单位、 块或函数的符号。|  
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|  
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|`DWORD`|终结点具有静态位置;有关详细信息，请参阅[符号位置](../../debugger/debug-interface-access/symbol-locations.md)枚举。|  
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|转换 （thunk） 的名称。|  
|[IDiaSymbol::get_pure](../../debugger/debug-interface-access/idiasymbol-get-pure.md)|`BOOL`|如果转换 （thunk） 完全是虚拟的 （仅在 DIA SDK V8.0 或更高版本），则为 TRUE。|  
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|此转换 （thunk） 其模块内的相对位置。|  
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|  
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagThunk`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|  
|[IDiaSymbol::get_targetOffset](../../debugger/debug-interface-access/idiasymbol-get-targetoffset.md)|`DWORD`|转换 （thunk） 目标的位置的偏移量的部分。|  
|[IDiaSymbol::get_targetRelativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-targetrelativevirtualaddress.md)|`DWORD`|其封闭块中的转换 （thunk） 目标的相对虚拟地址。|  
|[IDiaSymbol::get_targetSection](../../debugger/debug-interface-access/idiasymbol-get-targetsection.md)|`DWORD`|部分转换 （thunk） 目标的一部分。|  
|[IDiaSymbol::get_targetVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-targetvirtualaddress.md)|`ULONGLONG`|在可执行映像中的转换 （thunk） 目标位置。|  
|[IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)|`DWORD`|Thunk 定义的类型， [THUNK_ORDINAL 枚举](../../debugger/debug-interface-access/thunk-ordinal.md)。|  
|[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)|`IDiaSymbol*`|此转换 （thunk） （仅在 DIA SDK V8.0 或更高版本） 的类型。|  
|[IDiaSymbol::get_typeId](../../debugger/debug-interface-access/idiasymbol-get-typeid.md)|`DWORD`|类型符号 （仅在 DIA SDK V8.0 或更高版本） 的 ID。|  
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|`BOOL`|`TRUE` 如果转换 （thunk） 未对齐 （仅在 DIA SDK V8.0 或更高版本），|  
|[IDiaSymbol::get_virtual](../../debugger/debug-interface-access/idiasymbol-get-virtual.md)|`BOOL`|`TRUE` 如果转换 （thunk） 是虚拟的 （仅在 DIA SDK V8.0 或更高版本）。|  
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|`ULONGLONG`|此转换 （thunk） 的可执行映像中的位置。|  
|[IDiaSymbol::get_virtualBaseOffset](../../debugger/debug-interface-access/idiasymbol-get-virtualbaseoffset.md)|`DWORD`|为此转换 （thunk） （仅在 DIA SDK V8.0 或更高版本） 的虚拟表中的偏移量。|  
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|`BOOL`|`TRUE` 如果转换 （thunk） 标记为易失性 （仅在 DIA SDK V8.0 或更高版本）。|  
  
## <a name="see-also"></a>请参阅  
 [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)   
 [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)   
 [THUNK_ORDINAL 枚举](../../debugger/debug-interface-access/thunk-ordinal.md)
