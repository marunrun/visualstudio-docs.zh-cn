---
title: CompilandEnv |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- CompilandEnv symbol
ms.assetid: 808404bb-ece1-47f1-b9ea-c76d4d86ddd9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b935c9c79fd618c96f44b2660c274f657f81014e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62555203"
---
# <a name="compilandenv"></a>CompilandEnv
编译器可能包括使用符号的其他环境变量。 还有一个`SymTagCompilandEnv`为每个这些变量的符号。

## <a name="properties"></a>属性
 下表显示适用于此符号类型的属性。

|属性|数据类型|描述|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|父编译单位符号。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|变量的名称。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagCompilandEnv`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|
|[IDiaSymbol::get_value](../../debugger/debug-interface-access/idiasymbol-get-value.md)|`VARIANT`|变量的字符串值的内容 (`VT_BSTR`)。|

## <a name="see-also"></a>请参阅
- [编译单位](../../debugger/debug-interface-access/compiland.md)
- [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)