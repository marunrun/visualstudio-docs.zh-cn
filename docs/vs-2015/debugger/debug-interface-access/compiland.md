---
title: 编译单位 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- compiland symbol
- compilands, compiland symbol
ms.assetid: c798eb2b-664a-41ec-ae90-5e9d292507ca
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 579ac6a70b379364870425e78cee41ac0840a214
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68163996"
---
# <a name="compiland"></a>编译单位
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

还有一个`SymTagCompiland`符号将每个编译单位链接到.exe 文件。 编译单位信息用于分隔包含符号`SymTagCompiland`标记，而不加载其他编译单位符号可以检索，和与符号`SymTagCompilandDetails`标记，这可能需要加载其他符号。  
  
## <a name="properties"></a>属性  
 下表显示适用于此符号类型的属性。  
  
|属性|数据类型|描述|  
|--------------|---------------|-----------------|  
|[IDiaSymbol::get_editAndContinueEnabled](../../debugger/debug-interface-access/idiasymbol-get-editandcontinueenabled.md)|`BOOL`|`TRUE` 如果在编译上启用编辑并继续。|  
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|.Exe 文件的符号。|  
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|  
|[IDiaSymbol::get_libraryName](../../debugger/debug-interface-access/idiasymbol-get-libraryname.md)|`BSTR`|对象从加载的库或对象文件的名称。|  
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|编译单位的对象文件的文件名。|  
|[IDiaSymbol::get_sourceFileName](../../debugger/debug-interface-access/idiasymbol-get-sourcefilename.md)|`BSTR`|源代码文件的名称。|  
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|  
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagCompiland`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|  
  
## <a name="see-also"></a>请参阅  
 [CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)   
 [CompilandEnv](../../debugger/debug-interface-access/compilandenv.md)   
 [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
