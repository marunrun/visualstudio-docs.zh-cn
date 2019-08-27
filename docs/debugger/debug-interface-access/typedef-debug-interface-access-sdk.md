---
title: Typedef （调试接口访问 SDK） |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Typedef symbol [DIA SDK]
ms.assetid: 9ab441b9-cc72-47fa-83e2-87b3c2b891b4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f1928667be38cc2b0aa56800ca66924d6159f0c4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62853526"
---
# <a name="typedef-debug-interface-access-sdk"></a>Typedef（调试接口访问 SDK）
使用符号`SymTagTypedef`标记引入其他类型的名称。

## <a name="properties"></a>属性
 下表显示此符号类型的其他有效属性。

|属性|数据类型|描述|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md)|`DWORD`|之一[BasicType 枚举](../../debugger/debug-interface-access/basictype.md)值。|
|[IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)|`IDiaSymbol*`|类的 typedef，如果有父对象。|
|[IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)|`DWORD`|类父符号的 ID。|
|[IDiaSymbol::get_constructor](../../debugger/debug-interface-access/idiasymbol-get-constructor.md)|`BOOL`|`TRUE` 如果此 typedef 具有构造函数。|
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|`BOOL`|`TRUE` 如果此 typedef 标记为常量。|
|[IDiaSymbol::get_hasAssignmentOperator](../../debugger/debug-interface-access/idiasymbol-get-hasassignmentoperator.md)|`BOOL`|`TRUE` 如果此 typedef 具有赋值运算符。|
|[IDiaSymbol::get_hasCastOperator](../../debugger/debug-interface-access/idiasymbol-get-hascastoperator.md)|`BOOL`|`TRUE` 如果此 typedef 具有强制转换运算符。|
|[IDiaSymbol::get_hasNestedTypes](../../debugger/debug-interface-access/idiasymbol-get-hasnestedtypes.md)|`BOOL`|`TRUE` 如果此 typedef 具有嵌套的类型。|
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|`ULONGLONG`|此 typedef 以字节为单位的长度。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|将封闭的编译单位符号。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|typedef 的名称。|
|[IDiaSymbol::get_nested](../../debugger/debug-interface-access/idiasymbol-get-nested.md)|`BOOL`|`TRUE` 如果在词法范围内嵌套的 typedef。|
|[IDiaSymbol::get_overloadedOperator](../../debugger/debug-interface-access/idiasymbol-get-overloadedoperator.md)|`BOOL`|`TRUE` 如果此 typedef 重载的运算符。|
|[IDiaSymbol::get_packed](../../debugger/debug-interface-access/idiasymbol-get-packed.md)|`BOOL`|`TRUE` 如果此 typedef 打包。|
|[IDiaSymbol::get_reference](../../debugger/debug-interface-access/idiasymbol-get-reference.md)|`BOOL`|`TRUE` 如果此 typedef 引用。|
|[IDiaSymbol::get_scoped](../../debugger/debug-interface-access/idiasymbol-get-scoped.md)|`BOOL`|`TRUE` 如果此 typedef 是在非全局的词法范围内。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagTypedef`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|
|[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)|`IDiaSymbol*`|基础类型的符号。|
|[IDiaSymbol::get_typeId](../../debugger/debug-interface-access/idiasymbol-get-typeid.md)|`DWORD`|类型符号的 ID。|
|[IDiaSymbol::get_udtKind](../../debugger/debug-interface-access/idiasymbol-get-udtkind.md)|`DWORD`|之一[UdtKind 枚举](../../debugger/debug-interface-access/udtkind.md)值。|
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|`BOOL`|`TRUE` 如果此 typedef 不对齐。|
|[IDiaSymbol::get_virtualTableShape](../../debugger/debug-interface-access/idiasymbol-get-virtualtableshape.md)|`IDiaSymbol*`|描述虚拟表形状符号。|
|[IDiaSymbol::get_virtualTableShapeId](../../debugger/debug-interface-access/idiasymbol-get-virtualtableshapeid.md)|`DWORD`|虚拟表形状符号的 ID。|
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|`BOOL`|`TRUE` 如果此 typedef 标记为易失性。|

## <a name="remarks"></a>备注
 由于类、 指针或用户定义类型 (UDT)，可以表示一个 typedef，typedef 的符号共享属性与这些其他类型的符号相同。

## <a name="see-also"></a>请参阅
- [符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)