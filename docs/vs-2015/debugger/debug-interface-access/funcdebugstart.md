---
title: FuncDebugStart | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- FuncDebugStart symbol
- debugging [DIA SDK], start point
ms.assetid: 1cbc6ca5-87d0-4c30-a39e-0a9dc62ce1a9
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 19c2192df89c532a615a4b5298fbf6e39669c4f4
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65692293"
---
# <a name="funcdebugstart"></a>FuncDebugStart
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

如果函数具有定义的点处的调试是若要开始，点由具有的符号`SymTagFuncDebugStart`标记。  
  
## <a name="properties"></a>属性  
 下表显示适用于此符号类型的属性。  
  
|属性|数据类型|描述|  
|--------------|---------------|-----------------|  
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|偏移量部分的位置;有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|  
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|`DWORD`|位置; 部分一部分有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|  
|[IDiaSymbol::get_customCallingConvention](../../debugger/debug-interface-access/idiasymbol-get-customcallingconvention.md)|`BOOL`|`TRUE` 如果该函数使用自定义调用约定 （仅在 DIA SDK v8.0 或更高版本）。|  
|[IDiaSymbol::get_farReturn](../../debugger/debug-interface-access/idiasymbol-get-farreturn.md)|`BOOL`|`TRUE` 如果函数执行得返回了 （仅在 DIA SDK v8.0 或更高版本）。|  
|[IDiaSymbol::get_interruptReturn](../../debugger/debug-interface-access/idiasymbol-get-interruptreturn.md)|`BOOL`|`TRUE` 如果函数包含从中断 （仅在 DIA SDK v8.0 或更高版本） 返回。|  
|[IDiaSymbol::get_isStatic](../../debugger/debug-interface-access/idiasymbol-get-isstatic.md)|`BOOL`|`TRUE` 如果函数被标记为静态，（仅在 DIA SDK v8.0 或更高版本）。|  
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|将封闭函数的符号。|  
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|  
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|`DWORD`|起始点具有静态位置;有关详细信息，请参阅[符号位置](../../debugger/debug-interface-access/symbol-locations.md)。|  
|[IDiaSymbol::get_noInline](../../debugger/debug-interface-access/idiasymbol-get-noinline.md)|`BOOL`|`TRUE` 如果该函数使用指定[noinline](https://msdn.microsoft.com/library/f259d55b-dec7-4bde-8cf9-14521e4fdc42)属性 （仅在 DIA SDK v8.0 或更高版本）。|  
|[IDiaSymbol::get_noReturn](../../debugger/debug-interface-access/idiasymbol-get-noreturn.md)|`BOOL`|`TRUE` 如果该函数使用指定[noreturn](https://msdn.microsoft.com/library/9c6517e5-22d7-4051-9974-3d2200ae4d1d)属性 （仅在 DIA SDK v8.0 或更高版本）。|  
|[IDiaSymbol::get_notReached](../../debugger/debug-interface-access/idiasymbol-get-notreached.md)|`BOOL`|`TRUE` 如果 （仅在 DIA SDK v8.0 或更高版本），永远不会调用的函数。|  
|[IDiaSymbol::get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md)|`LONG`|在内存中; 符号的偏移量有关详细信息，请参阅[LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)， `LocIsRegRel`。|  
|[IDiaSymbol::get_optimizedCodeDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-optimizedcodedebuginfo.md)|`BOOL`|`TRUE` 如果代码具有为优化代码 （仅在 DIA SDK v8.0 或更高版本） 的调试信息。|  
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|它的块中的函数的相对位置。|  
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|  
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagFuncDebugStart`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|  
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|`ULONGLONG`|可执行文件中的函数的位置。|  
  
## <a name="see-also"></a>请参阅  
 [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)   
 [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)   
 [符号位置](../../debugger/debug-interface-access/symbol-locations.md)
