---
title: BaseClass |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- user-defined types, base classes
- BaseClass symbol
- base classes, user-defined types
ms.assetid: 9375ca35-cb91-45f5-8903-7344ee4528e8
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 61b08d18f694bf43708c58a8e378c8fc0ef283cb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62552574"
---
# <a name="baseclass"></a>BaseClass
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

每个基类的用户定义类型 (UDT) 符号由具有的子项`SymTagBaseClass`标记。 [Idiasymbol:: Get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)属性为基础的 UDT，包含的符号和用户定义的基础类型的所有属性都均可作为此 BaseClass 符号的一部分。  
  
## <a name="properties"></a>属性  
 下表显示此符号类型的其他有效属性。  
  
|属性|数据类型|描述|  
|--------------|---------------|-----------------|  
|[IDiaSymbol::get_access](../../debugger/debug-interface-access/idiasymbol-get-access.md)|`DWORD`|应用于此基类的访问修饰符。 之一[CV_access_e 枚举](../../debugger/debug-interface-access/cv-access-e.md)值。|  
|[IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)|`IDiaSymbol*`|封闭类 （如果有） 的符号。|  
|[IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)|`DWORD`|类父符号的 ID。|  
|[IDiaSymbol::get_constructor](../../debugger/debug-interface-access/idiasymbol-get-constructor.md)|`BOOL`|`TRUE` 如果基的类具有构造函数。|  
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|`BOOL`|`TRUE` 如果基的类被标记为常量。|  
|[IDiaSymbol::get_hasAssignmentOperator](../../debugger/debug-interface-access/idiasymbol-get-hasassignmentoperator.md)|`BOOL`|`TRUE` 如果基类不包含赋值运算符。|  
|[IDiaSymbol::get_hasCastOperator](../../debugger/debug-interface-access/idiasymbol-get-hascastoperator.md)|`BOOL`|`TRUE` 如果基类具有一个强制转换运算符。|  
|[IDiaSymbol::get_hasNestedTypes](../../debugger/debug-interface-access/idiasymbol-get-hasnestedtypes.md)|`BOOL`|`TRUE` 如果基类具有嵌套的类型。|  
|[IDiaSymbol::get_indirectVirtualBaseClass](../../debugger/debug-interface-access/idiasymbol-get-indirectvirtualbaseclass.md)|`BOOL`|`TRUE` 如果是间接的基类。|  
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|`DWORD`|此基类以字节为单位的长度。|  
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|将封闭的编译单位符号。|  
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|  
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|基类的名称。|  
|[IDiaSymbol::get_nested](../../debugger/debug-interface-access/idiasymbol-get-nested.md)|`BOOL`|`TRUE` 如果嵌套的类的基类。|  
|[IDiaSymbol::get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md)|`LONG`|表示结构中的基类的子对象的偏移量。|  
|[IDiaSymbol::get_overloadedOperator](../../debugger/debug-interface-access/idiasymbol-get-overloadedoperator.md)|`BOOL`|`TRUE` 如果基类不包含任何重载的运算符。|  
|[IDiaSymbol::get_packed](../../debugger/debug-interface-access/idiasymbol-get-packed.md)|`BOOL`|`TRUE` 如果压缩的基类。|  
|[IDiaSymbol::get_scoped](../../debugger/debug-interface-access/idiasymbol-get-scoped.md)|`BOOL`|`TRUE` 如果非全局作用域中出现的基类。|  
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|  
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagBaseClass`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|  
|[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)|`IDiaSymbol*`|类的基类的符号[UDT](../../debugger/debug-interface-access/udt.md)。|  
|[IDiaSymbol::get_typeId](../../debugger/debug-interface-access/idiasymbol-get-typeid.md)|`DWORD`|类型符号的 ID。|  
|[IDiaSymbol::get_udtKind](../../debugger/debug-interface-access/idiasymbol-get-udtkind.md)|`DWORD`|中的值[UdtKind 枚举](../../debugger/debug-interface-access/udtkind.md)。|  
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|`BOOL`|`TRUE` 如果未对齐的基类。|  
|[IDiaSymbol::get_virtualBaseClass](../../debugger/debug-interface-access/idiasymbol-get-virtualbaseclass.md)|`BOOL`|`TRUE` 如果是虚拟的基类。|  
|[IDiaSymbol::get_virtualBaseDispIndex](../../debugger/debug-interface-access/idiasymbol-get-virtualbasedispindex.md)|`DWORD`|中的虚拟基的偏移量表的索引。|  
|[IDiaSymbol::get_virtualBasePointerOffset](../../debugger/debug-interface-access/idiasymbol-get-virtualbasepointeroffset.md)|`LONG`|虚拟基指针的偏移量。|  
|[IDiaSymbol::get_virtualBaseTableType](../../debugger/debug-interface-access/idiasymbol-get-virtualbasetabletype.md)|`IDiaSymbol*`|虚拟表，基指针的类型。|  
|[IDiaSymbol::get_virtualTableShape](../../debugger/debug-interface-access/idiasymbol-get-virtualtableshape.md)|`IDiaSymbol*`|描述此基类的虚拟表的类型符号。|  
|[IDiaSymbol::get_virtualTableShapeId](../../debugger/debug-interface-access/idiasymbol-get-virtualtableshapeid.md)|`DWORD`|虚拟表形状符号的 ID。|  
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|`BOOL`|`TRUE` 如果类的基类被标记为易失性。|  
  
## <a name="see-also"></a>请参阅  
 [符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)   
 [UDT](../../debugger/debug-interface-access/udt.md)
