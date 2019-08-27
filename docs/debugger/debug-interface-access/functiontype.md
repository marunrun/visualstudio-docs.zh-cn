---
title: FunctionType |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- function signature
- FunctionType symbol
ms.assetid: 646a07e7-9d4f-4e21-95e3-3e403cdd4843
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8913d9b26ab79a37e9d6f28a5f3bf1974df15a5f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62554451"
---
# <a name="functiontype"></a>FunctionType
每个唯一函数签名由`SymTagFunctionType`符号。 每个参数标识为具有的类子符号`SymTagFunctionArgType`标记。

## <a name="properties"></a>属性
 下表显示此符号类型的其他有效属性。

|属性|数据类型|描述|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)|`DWORD`|值之一[CV_call_e 枚举](../../debugger/debug-interface-access/cv-call-e.md)。|
|[IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)|`IDiaSymbol*`|此函数 （或方法） 是的成员的类。|
|[IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)|`DWORD`|类父符号的 ID。|
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|`BOOL`|`TRUE` 如果该函数标记为常量。|
|[IDiaSymbol::get_count](../../debugger/debug-interface-access/idiasymbol-get-count.md)|`DWORD`|函数参数的数目。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|将封闭的编译单位符号。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|
|[IDiaSymbol::get_objectPointerType](../../debugger/debug-interface-access/idiasymbol-get-objectpointertype.md)|`IDiaSymbol*`|该方法的对象指针 ("this") 的类型。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagFunctionType`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|
|[IDiaSymbol::get_thisAdjust](../../debugger/debug-interface-access/idiasymbol-get-thisadjust.md)|`LONG`|逻辑"this"精算师方法。|
|[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)|`IDiaSymbol*`|返回值类型的符号。|
|[IDiaSymbol::get_typeId](../../debugger/debug-interface-access/idiasymbol-get-typeid.md)|`DWORD`|类型符号的 ID。|
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|`BOOL`|`TRUE` 如果函数未对齐。|
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|`BOOL`|`TRUE` 如果该函数标记为易失性。|

## <a name="see-also"></a>请参阅
- [符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)
- [CV_access_e 枚举](../../debugger/debug-interface-access/cv-access-e.md)
- [FunctionArgType](../../debugger/debug-interface-access/functionargtype.md)