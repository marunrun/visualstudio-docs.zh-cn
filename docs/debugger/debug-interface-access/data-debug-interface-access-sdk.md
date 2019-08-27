---
title: 数据 （调试接口访问 SDK） |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- global variables [C++], as symbols
- local variables [C++], as symbols
- class members [C++], as symbols
- Data symbol
ms.assetid: 0f17e96a-2e06-42c9-a877-3e5e670ee0ef
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6f0cf6e4f02d8a80f74d0edb46e188b41bfb425c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62554943"
---
# <a name="data-debug-interface-access-sdk"></a>数据（调试界面访问 SDK）
所有变量，如参数、 局部变量、 全局变量和类成员，由都标识`SymTagData`符号。 常量值 (`LocIsConstant`) 还可以标识与此类型。

## <a name="properties"></a>属性
 下表显示适用于此符号类型的属性。

|属性|数据类型|描述|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_access](../../debugger/debug-interface-access/idiasymbol-get-access.md)|`DWORD`|如果一个字段，然后的值之一[CV_access_e 枚举](../../debugger/debug-interface-access/cv-access-e.md)。|
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|偏移量部分的位置;有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|`DWORD`|位置; 部分一部分有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_addressTaken](../../debugger/debug-interface-access/idiasymbol-get-addresstaken.md)|`BOOL`|`TRUE` 如果此数据的地址被引用的另一个符号。|
|[IDiaSymbol::get_bitPosition](../../debugger/debug-interface-access/idiasymbol-get-bitposition.md)|`DWORD`|位位置的位置;有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)（不支持在 DIA SDK v8.0）。|
|[IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)|`IDiaSymbol*`|对于类，如果这是结构、 联合或类字段的符号。|
|[IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)|`DWORD`|类父符号的 ID。|
|[IDiaSymbol::get_compilerGenerated](../../debugger/debug-interface-access/idiasymbol-get-compilergenerated.md)|`BOOL`|`TRUE` 如果数据由编译器生成的。|
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|`BOOL`|`TRUE` 如果数据被标记为常量。|
|[IDiaSymbol::get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md)|`DWORD`|之一[DataKind 枚举](../../debugger/debug-interface-access/datakind.md)值。|
|[IDiaSymbol::get_isAggregated](../../debugger/debug-interface-access/idiasymbol-get-isaggregated.md)|`BOOL`|`TRUE` 如果数据是聚合的数据类型 （仅在 DIA SDK v8.0 及更高版本） 的一部分。|
|[IDiaSymbol::get_isSplitted](../../debugger/debug-interface-access/idiasymbol-get-issplitted.md)|`BOOL`|`TRUE` 如果数据已被拆分为多个符号 （仅在 DIA SDK v8.0 及更高版本） 的聚合。|
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|`ULONGLONG`|位域; 的长度有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|封闭的编译单位、 函数或块的符号。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|`DWORD`|任何允许的位置类型;有关详细信息，请参阅[符号位置](../../debugger/debug-interface-access/symbol-locations.md)|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|变量的名称。|
|[IDiaSymbol::get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md)|`LONG`|相对于寄存器内容; 偏移量有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_registerId](../../debugger/debug-interface-access/idiasymbol-get-registerid.md)|`DWORD`|注册位置; 指示的符有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|它的块中的数据的相对位置。|
|[IDiaSymbol::get_slot](../../debugger/debug-interface-access/idiasymbol-get-slot.md)|`DWORD`|获取数据的槽数。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagData`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|
|[IDiaSymbol::get_token](../../debugger/debug-interface-access/idiasymbol-get-token.md)|`DWORD`|表示数据的元数据标记。|
|[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)|`IDiaSymbol*`|变量类型的符号。|
|[IDiaSymbol::get_typeId](../../debugger/debug-interface-access/idiasymbol-get-typeid.md)|`DWORD`|变量类型符号的 ID。|
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|`BOOL`|`TRUE` 如果数据未对齐。|
|[IDiaSymbol::get_value](../../debugger/debug-interface-access/idiasymbol-get-value.md)|`VARIANT`|常量数据的值。|
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|`ULONGLONG`|可执行文件中的数据的位置。|
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|`BOOL`|`TRUE` 如果数据被标记为易失性。|

## <a name="see-also"></a>请参阅
- [CV_access_e 枚举](../../debugger/debug-interface-access/cv-access-e.md)
- [DataKind 枚举](../../debugger/debug-interface-access/datakind.md)
- [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)
- [符号位置](../../debugger/debug-interface-access/symbol-locations.md)