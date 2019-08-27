---
title: VTable | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- VTable symbol
- virtual tables
ms.assetid: c8be6692-7d2a-4721-99d3-8e2e565bb8a1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f1f630c744a799183fe790e8b3067d0fc13378bc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62853308"
---
# <a name="vtable"></a>VTable
虚拟表由`SymTagVTable`符号。

## <a name="properties"></a>属性
 下表显示此符号类型的其他有效属性。

|属性|数据类型|描述|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)|`IDiaSymbol*`|拥有此 VTable 的类的符号。|
|[IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)|`DWORD`|类父符号的 ID。|
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|`BOOL`|`TRUE` 如果的 VTable 类标记为常量。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|将封闭的编译单位符号。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagVTable`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|
|[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)|`IDiaSymbol*`|VTable 符号[VTableShape](../../debugger/debug-interface-access/vtableshape.md)。|
|[IDiaSymbol::get_typeId](../../debugger/debug-interface-access/idiasymbol-get-typeid.md)|`DWORD`|类型符号的 ID。|
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|`BOOL`|`TRUE` 如果此类的 VTable 是未对齐。|
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|`BOOL`|`TRUE` 如果的 VTable 类标记为易失性。|

## <a name="see-also"></a>请参阅
- [符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)
- [VTableShape](../../debugger/debug-interface-access/vtableshape.md)