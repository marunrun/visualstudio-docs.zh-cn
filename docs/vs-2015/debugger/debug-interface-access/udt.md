---
title: UDT | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- SymTagUDT symbol
- user-defined type (UDT) symbol
- unions, as symbols
- UDT symbol
- structs [C++]
ms.assetid: f12459dd-c64d-4cc9-9ee3-a56e19e9e573
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 97a0df64f06a8e0530884c5e1b532763066c709b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202394"
---
# <a name="udt"></a>UDT
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

每个类、 结构和联合由`SymTagUDT`符号。 每个成员、 函数、 数据或嵌套的类型和每个基类，显示为类子项的用户定义类型 (UDT)。  
  
## <a name="properties"></a>属性  
 下表显示此符号类型的其他有效属性。  
  
|Property|数据类型|描述|  
|--------------|---------------|-----------------|  
|[IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)|`IDiaSymbol*`|类父，如果任何符号。|  
|[IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)|`DWORD`|类父符号的 ID。|  
|[IDiaSymbol::get_constructor](../../debugger/debug-interface-access/idiasymbol-get-constructor.md)|`BOOL`|`TRUE` 用户定义的类型是否包含构造函数。|  
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|`BOOL`|`TRUE` 如果用户定义的类型被标记为常量。|  
|[IDiaSymbol::get_hasAssignmentOperator](../../debugger/debug-interface-access/idiasymbol-get-hasassignmentoperator.md)|`BOOL`|`TRUE` 如果 UDT 定义任何赋值运算符。|  
|[IDiaSymbol::get_hasCastOperator](../../debugger/debug-interface-access/idiasymbol-get-hascastoperator.md)|`BOOL`|`TRUE` 如果 UDT 定义任何强制转换运算符。|  
|[IDiaSymbol::get_hasNestedTypes](../../debugger/debug-interface-access/idiasymbol-get-hasnestedtypes.md)|`BOOL`|`TRUE` 如果用户定义的类型具有嵌套的类型的定义。|  
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|`LONGLONG`|以字节为单位，UDT 的大小。|  
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|封闭符号[编译单位](../../debugger/debug-interface-access/compiland.md)。|  
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|  
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|UDT 的名称。|  
|[IDiaSymbol::get_nested](../../debugger/debug-interface-access/idiasymbol-get-nested.md)|`BOOL`|`TRUE` 如果嵌套 UDT。|  
|[IDiaSymbol::get_overloadedOperator](../../debugger/debug-interface-access/idiasymbol-get-overloadedoperator.md)|`BOOL`|`TRUE` 如果 udt 定义重载的运算符。|  
|[IDiaSymbol::get_packed](../../debugger/debug-interface-access/idiasymbol-get-packed.md)|`BOOL`|`TRUE` 如果压缩用户定义的类型。|  
|[IDiaSymbol::get_scoped](../../debugger/debug-interface-access/idiasymbol-get-scoped.md)|`BOOL`|`TRUE` 如果用户定义的类型出现在非全局的词法范围内。|  
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|  
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagUDT`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|  
|[IDiaSymbol::get_udtKind](../../debugger/debug-interface-access/idiasymbol-get-udtkind.md)|`DWORD`|指示这是结构、 类或; 并集有关详细信息，请参阅[UdtKind 枚举](../../debugger/debug-interface-access/udtkind.md)。|  
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|`BOOL`|`TRUE` 如果 UDT 是未对齐。|  
|[IDiaSymbol::get_virtualTableShape](../../debugger/debug-interface-access/idiasymbol-get-virtualtableshape.md)|`IDiaSymbol*`|虚拟表的类型。|  
|[IDiaSymbol::get_virtualTableShapeId](../../debugger/debug-interface-access/idiasymbol-get-virtualtableshapeid.md)|`DWORD`|虚拟表形状符号的 ID。|  
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|`BOOL`|`TRUE` 如果用户定义的类型被标记为易失性。|  
  
## <a name="see-also"></a>请参阅  
 [符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)
