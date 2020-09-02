---
title: 自定义 (调试接口访问 SDK) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- Custom symbol
ms.assetid: a219fc83-d2a8-4bc5-b7e1-bfafeb247f16
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5e1a1819178961ae0a4ccd02286d6a166fd18b8f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68164398"
---
# <a name="custom-debug-interface-access-sdk"></a>自定义（调试接口访问 SDK）
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

某些编译器会引入未由任何标准词法符号类型标识的符号。 这些符号由 `SymTagCustom` 标记标识。  
  
## <a name="properties"></a>属性  
 下表显示了对此符号类型有效的属性。  
  
|属性|数据类型|说明|  
|--------------|---------------|-----------------|  
|[IDiaSymbol::get_dataBytes](../../debugger/debug-interface-access/idiasymbol-get-databytes.md)|`BYTE`|与符号关联的数据数组。|  
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|符号的索引 ID。|  
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回 `SymTagCustom` () 的 [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md) 值之一。|  
  
## <a name="see-also"></a>另请参阅  
 [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
