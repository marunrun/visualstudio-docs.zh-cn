---
title: BaseType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- BaseType symbol [DIA SDK]
ms.assetid: 2f9e22e6-8360-496a-ac6b-17a5a56b0c46
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8e7057d0a75252583ceb1d538aa71a46b65991b9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829903"
---
# <a name="basetype"></a>BaseType
基类型进行标识`SymTagBaseType`符号。

## <a name="properties"></a>属性
 下表显示此符号类型的其他有效属性。

|属性|数据类型|描述|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md)|`DWORD`|值之一[BasicType 枚举](../../debugger/debug-interface-access/basictype.md)。|
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|`BOOL`|`TRUE` 如果基类型被标记为常量。|
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|`LONGLONG`|大小，以字节为单位的基类型。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|封闭符号[编译单位](../../debugger/debug-interface-access/compiland.md)。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagBaseType`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|`BOOL`|`TRUE` 如果基类型是未对齐。|
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|`BOOL`|`TRUE` 如果基类型被标记为易失性。|

## <a name="see-also"></a>请参阅
- [BasicType 枚举](../../debugger/debug-interface-access/basictype.md)
- [符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)