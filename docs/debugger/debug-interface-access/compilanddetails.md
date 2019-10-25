---
title: CompilandDetails |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- CompilandDetails symbol
ms.assetid: ddc7d794-c622-4c63-b2a6-72f8b2d0022a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b72a5ae53c336877c68cc9b164cf787017dacbe2
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745418"
---
# <a name="compilanddetails"></a>CompilandDetails
编译单位信息在带有 `SymTagCompiland` 标记的符号（低细节）和 `SymTagCompilandDetails` 标记（高详细）之间进行拆分。 `SymTagCompilandDetails` 需要加载其他符号。 不过，它提供了大量有关 `SymTagCompiland` 符号不可用的编译单位信息。

## <a name="properties"></a>属性
 下表显示了对此符号类型有效的属性。

|Property|数据类型|描述|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_backEndBuild](../../debugger/debug-interface-access/idiasymbol-get-backendbuild.md)|`DWORD`|编译器的后端内部版本号。|
|[IDiaSymbol::get_backEndMajor](../../debugger/debug-interface-access/idiasymbol-get-backendmajor.md)|`DWORD`|编译器的后端主版本号。|
|[IDiaSymbol::get_backEndMinor](../../debugger/debug-interface-access/idiasymbol-get-backendminor.md)|`DWORD`|编译器的后端次版本号。|
|[IDiaSymbol::get_compilerName](../../debugger/debug-interface-access/idiasymbol-get-compilername.md)|`BSTR`|生成此编译单位的编译器的名称（仅在 DIA SDK 8.0 或更高版本中）。|
|[IDiaSymbol::get_editAndContinueEnabled](../../debugger/debug-interface-access/idiasymbol-get-editandcontinueenabled.md)|`BOOL`|如果在编译时启用了 "编辑并继续"，则 `TRUE`。|
|[IDiaSymbol::get_frontEndBuild](../../debugger/debug-interface-access/idiasymbol-get-frontendbuild.md)|`DWORD`|编译器的前端内部版本号。|
|[IDiaSymbol::get_frontEndMajor](../../debugger/debug-interface-access/idiasymbol-get-frontendmajor.md)|`DWORD`|编译器的前端主版本号。|
|[IDiaSymbol::get_frontEndMinor](../../debugger/debug-interface-access/idiasymbol-get-frontendminor.md)|`DWORD`|编译器的前端次版本号。|
|[IDiaSymbol::get_hasDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-hasdebuginfo.md)|`BOOL`|如果此编译单位具有调试信息，则 `TRUE` （仅在 DIA SDK v2.0 或更高版本中）。|
|[IDiaSymbol::get_hasManagedCode](../../debugger/debug-interface-access/idiasymbol-get-hasmanagedcode.md)|`BOOL`|如果此编译单位包含托管代码，则 `TRUE` （仅在 DIA SDK v2.0 或更高版本中）。|
|[IDiaSymbol::get_hasSecurityChecks](../../debugger/debug-interface-access/idiasymbol-get-hassecuritychecks.md)|`BOOL`|`TRUE` 如果编译单位是用[/gs （缓冲区安全检查）](/cpp/build/reference/gs-buffer-security-check)编译器开关编译的（仅在 DIA SDK v2.0 或更高版本中）。|
|[IDiaSymbol::get_isCVTCIL](../../debugger/debug-interface-access/idiasymbol-get-iscvtcil.md)|`BOOL`|`TRUE` 如果编译单位已从公共中间语言（CIL）代码转换为本机代码，则为。|
|[IDiaSymbol::get_isDataAligned](../../debugger/debug-interface-access/idiasymbol-get-isdataaligned.md)|`BOOL`|`TRUE` 如果用户定义类型（UDT）已与某个指定的内存边界对齐（仅在 DIA SDK v2.0 或更高版本中）。|
|[IDiaSymbol::get_isHotpatchable](../../debugger/debug-interface-access/idiasymbol-get-ishotpatchable.md)|`BOOL`|`TRUE` 如果编译单位是用[/hotpatch （Create 可热修补 Image）](/cpp/build/reference/hotpatch-create-hotpatchable-image)编译器开关编译的（仅在 DIA SDK v2.0 或更高版本中）。|
|[IDiaSymbol::get_isLTCG](../../debugger/debug-interface-access/idiasymbol-get-isltcg.md)|`BOOL`|`TRUE` 如果编译单位是用[/ltcg （链接时间代码生成）](/cpp/build/reference/ltcg-link-time-code-generation)编译器开关编译的（仅在 DIA SDK v2.0 或更高版本中）。|
|[IDiaSymbol::get_isMSILNetmodule](../../debugger/debug-interface-access/idiasymbol-get-ismsilnetmodule.md)|`BOOL`|如果编译单位是 Microsoft 中间语言（MSIL）模块（仅在 DIA SDK 8.0 或更高版本中），则为 TRUE。|
|[IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)|`DWORD`|源代码语言。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|编译单位的符号。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|
|[IDiaSymbol::get_platform](../../debugger/debug-interface-access/idiasymbol-get-platform.md)|`DWORD`|编译编译单位的平台（ [CV_CPU_TYPE_e 枚举](../../debugger/debug-interface-access/cv-cpu-type-e.md)值之一）。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|符号的索引 ID。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回 `SymTagCompilandDetails` （ [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值之一）。|

## <a name="remarks"></a>备注
 编译器通常以称为两遍编译器的形式提供;在某些编译器版本中，每个传递都由单独的程序处理。 它们分别称为前端和后端编译器，因此是后端版本号和前端版本号的符号属性。

## <a name="see-also"></a>请参阅
- [编译单位](../../debugger/debug-interface-access/compiland.md)
- [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)