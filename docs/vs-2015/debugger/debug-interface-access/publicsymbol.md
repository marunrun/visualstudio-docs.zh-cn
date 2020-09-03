---
title: PublicSymbol |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- data symbols [C++]
- PublicSymbol symbol
- global functions [C++], as public symbols
ms.assetid: f8d33007-302d-4549-9dad-47fb33ea60b7
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8f36480dc8ddaac3d9977155f2b1a7741ebe3ba1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68155594"
---
# <a name="publicsymbol"></a>PublicSymbol
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

创建 .exe 文件时，每个公共符号 (最少，每个全局函数和数据符号) 均为 `SymTagPublicSymbol` 标记。  
  
## <a name="properties"></a>属性  
 下表显示了对此符号类型有效的属性。  
  
|属性|数据类型|说明|  
|--------------|---------------|-----------------|  
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|Location 的偏移量部分;有关详细信息，请参阅 [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|  
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|`DWORD`|位置部分;有关详细信息，请参阅 [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|  
|[IDiaSymbol::get_code](../../debugger/debug-interface-access/idiasymbol-get-code.md)|`BOOL`|`TRUE` 符号在代码中的位置。|  
|[IDiaSymbol::get_function](../../debugger/debug-interface-access/idiasymbol-get-function.md)|`BOOL`|`TRUE` 如果符号是函数，则为。|  
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|`ULONGLONG`|此符号的长度（以字节为单位）。|  
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|全局范围的符号。|  
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|  
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|`DWORD`|公共符号具有静态位置;有关详细信息，请参阅 [符号位置](../../debugger/debug-interface-access/symbol-locations.md)。|  
|[IDiaSymbol::get_managed](../../debugger/debug-interface-access/idiasymbol-get-managed.md)|`BOOL`|`TRUE` 符号在托管代码中的位置。|  
|[IDiaSymbol::get_msil](../../debugger/debug-interface-access/idiasymbol-get-msil.md)|`BOOL`|`TRUE` 如果符号的位置为 Microsoft 中间语言 (MSIL) 代码。|  
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|符号的完全修饰名。|  
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|符号的索引 ID。|  
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|符号在其块中的相对位置。|  
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回 `SymTagPublicSymbol` () 的 [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md) 值之一。|  
|[IDiaSymbol::get_undecoratedName](../../debugger/debug-interface-access/idiasymbol-get-undecoratedname.md)|`BSTR`|未修饰符号名称。|  
|[IDiaSymbol::get_undecoratedNameEx](../../debugger/debug-interface-access/idiasymbol-get-undecoratednameex.md)|`BSTR`|部分或全部未修饰符号名称。|  
  
## <a name="see-also"></a>另请参阅  
 [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)   
 [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)   
 [符号位置](../../debugger/debug-interface-access/symbol-locations.md)
