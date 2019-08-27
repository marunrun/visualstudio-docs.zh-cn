---
title: Exe | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- .dll files
- Exe symbol
- .exe files
- executable files, Exe symbol
ms.assetid: a781d2cf-55fe-4373-9cf1-b732864244e0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6078f4dae6bc6fb53dfa8b612972e28edd820f72
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62554748"
---
# <a name="exe"></a>Exe
Exe 是唯一的符号不带词法或类父级，因为它表示全局范围的.exe 或.dll 文件。 没有具有只有一个符号`SymTagExe`标记每个文件。 [Idiasession:: Get_globalscope](../../debugger/debug-interface-access/idiasession-get-globalscope.md)方法返回的符号。

## <a name="properties"></a>属性
 下表显示适用于此符号类型的属性。

|属性|数据类型|描述|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_age](../../debugger/debug-interface-access/idiasymbol-get-age.md)|`DWORD`|此可执行文件的年龄。|
|[IDiaSymbol::get_guid](../../debugger/debug-interface-access/idiasymbol-get-guid.md)|`GUID`|`GUID` 此可执行文件。|
|[IDiaSymbol::get_isCTypes](../../debugger/debug-interface-access/idiasymbol-get-isctypes.md)|`BOOL`|`TRUE` 如果符号文件与此可执行文件将包含 C 类型 （仅在 DIA SDK v8.0 或更高版本）。|
|[IDiaSymbol::get_isStripped](../../debugger/debug-interface-access/idiasymbol-get-isstripped.md)|`BOOL`|`TRUE` 如果从与此可执行文件 （仅在 DIA SDK v8.0 或更高版本） 关联的符号文件中有已去除私有符号。|
|[IDiaSymbol::get_machineType](../../debugger/debug-interface-access/idiasymbol-get-machinetype.md)|`DWORD`|值，该值指示目标 CPU (之一[CV_CPU_TYPE_e 枚举](../../debugger/debug-interface-access/cv-cpu-type-e.md)值)。|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|.Exe 文件的名称。|
|[IDiaSymbol::get_signature](../../debugger/debug-interface-access/idiasymbol-get-signature.md)|`DWORD`|可执行文件的签名。|
|[IDiaSymbol::get_symbolsFileName](../../debugger/debug-interface-access/idiasymbol-get-symbolsfilename.md)|`BSTR`|.Exe 文件的.pdb 或.dbg 文件的完整路径。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagExe`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|

## <a name="see-also"></a>请参阅
- [IDiaSession::get_globalScope](../../debugger/debug-interface-access/idiasession-get-globalscope.md)
- [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)