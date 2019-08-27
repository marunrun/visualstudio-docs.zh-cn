---
title: VTableShape | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- VTableShape symbol
- SymTagVTableShape tag
ms.assetid: dd97f4c3-115d-46a9-b506-2531e30a0d8f
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2716a01f86a095c9378d7806cfa71fff3bc51a8d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68183562"
---
# <a name="vtableshape"></a>VTableShape
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[VTable](../../debugger/debug-interface-access/vtable.md)符号具有标识的类子符号`SymTagVTableShape`标记。  
  
## <a name="properties"></a>属性  
 下表显示此符号类型的其他有效属性。  
  
|属性|数据类型|描述|  
|--------------|---------------|-----------------|  
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|`BOOL`|`TRUE` 如果的 VTable 类标记为常量。|  
|[IDiaSymbol::get_count](../../debugger/debug-interface-access/idiasymbol-get-count.md)|`DWORD`|VTable 中的条目数。|  
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|将封闭的编译单位符号。|  
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|  
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|  
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagVTableShape`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|  
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|`BOOL`|`TRUE` 如果此类的 VTable 是未对齐。|  
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|`BOOL`|`TRUE` 如果的 VTable 类标记为易失性。|  
  
## <a name="see-also"></a>请参阅  
 [符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)   
 [VTable](../../debugger/debug-interface-access/vtable.md)
