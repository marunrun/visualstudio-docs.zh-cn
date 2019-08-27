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
ms.openlocfilehash: 896832ac3e96e499aa564d5bce44dc06185090de
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62555242"
---
# <a name="compilanddetails"></a>CompilandDetails
编译单位信息用于分隔包含符号`SymTagCompiland`标记 （低详细信息） 和一个`SymTagCompilandDetails`标记 （高详细信息）。 `SymTagCompilandDetails` 需要加载其他符号。 但是，它提供了丰富的信息不适用于编译单位`SymTagCompiland`符号。

## <a name="properties"></a>属性
 下表显示适用于此符号类型的属性。

|属性|数据类型|描述|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_backEndBuild](../../debugger/debug-interface-access/idiasymbol-get-backendbuild.md)|`DWORD`|编译器后端内部版本号。|
|[IDiaSymbol::get_backEndMajor](../../debugger/debug-interface-access/idiasymbol-get-backendmajor.md)|`DWORD`|后端主要编译器的版本号。|
|[IDiaSymbol::get_backEndMinor](../../debugger/debug-interface-access/idiasymbol-get-backendminor.md)|`DWORD`|后端次版本号的编译器。|
|[IDiaSymbol::get_compilerName](../../debugger/debug-interface-access/idiasymbol-get-compilername.md)|`BSTR`|编译器生成此编译单位 （仅在 DIA SDK V8.0 或更高版本） 的名称。|
|[IDiaSymbol::get_editAndContinueEnabled](../../debugger/debug-interface-access/idiasymbol-get-editandcontinueenabled.md)|`BOOL`|`TRUE` 如果在编译已启用编辑并继续。|
|[IDiaSymbol::get_frontEndBuild](../../debugger/debug-interface-access/idiasymbol-get-frontendbuild.md)|`DWORD`|编译器前端生成号。|
|[IDiaSymbol::get_frontEndMajor](../../debugger/debug-interface-access/idiasymbol-get-frontendmajor.md)|`DWORD`|前端主要编译器的版本号。|
|[IDiaSymbol::get_frontEndMinor](../../debugger/debug-interface-access/idiasymbol-get-frontendminor.md)|`DWORD`|前端次版本号的编译器。|
|[IDiaSymbol::get_hasDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-hasdebuginfo.md)|`BOOL`|`TRUE` 如果此编译单位包含调试信息 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_hasManagedCode](../../debugger/debug-interface-access/idiasymbol-get-hasmanagedcode.md)|`BOOL`|`TRUE` 如果此编译单位中包含托管的代码 （仅在 DIA SDK v8.0 或更高版本）。|
|[IDiaSymbol::get_hasSecurityChecks](../../debugger/debug-interface-access/idiasymbol-get-hassecuritychecks.md)|`BOOL`|`TRUE` 如果使用编译时将编译单位[/GS （缓冲区安全检查）](/cpp/build/reference/gs-buffer-security-check)编译器开关 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_isCVTCIL](../../debugger/debug-interface-access/idiasymbol-get-iscvtcil.md)|`BOOL`|`TRUE` 如果编译单位从公共中间语言 (CIL) 代码转换为本机代码。|
|[IDiaSymbol::get_isDataAligned](../../debugger/debug-interface-access/idiasymbol-get-isdataaligned.md)|`BOOL`|`TRUE` 如果已与用户定义类型 (UDT) 对齐到某些指定内存边界 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_isHotpatchable](../../debugger/debug-interface-access/idiasymbol-get-ishotpatchable.md)|`BOOL`|`TRUE` 如果使用编译时编译单位[/hotpatch （创建可热修补映像）](/cpp/build/reference/hotpatch-create-hotpatchable-image)编译器开关 （仅在 DIA SDK v8.0 或更高版本）。|
|[IDiaSymbol::get_isLTCG](../../debugger/debug-interface-access/idiasymbol-get-isltcg.md)|`BOOL`|`TRUE` 如果使用编译时编译单位[/LTCG （链接时间代码生成）](/cpp/build/reference/ltcg-link-time-code-generation)编译器开关 （仅在 DIA SDK V8.0 或更高版本）。|
|[IDiaSymbol::get_isMSILNetmodule](../../debugger/debug-interface-access/idiasymbol-get-ismsilnetmodule.md)|`BOOL`|如果编译单位是一个 Microsoft 中间语言 (MSIL) 模块 （仅在 DIA SDK v8.0 或更高版本），则为 TRUE。|
|[IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)|`DWORD`|源代码语言。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|将编译单位符号。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|
|[IDiaSymbol::get_platform](../../debugger/debug-interface-access/idiasymbol-get-platform.md)|`DWORD`|平台编译将编译单位 (之一[CV_CPU_TYPE_e 枚举](../../debugger/debug-interface-access/cv-cpu-type-e.md)值)。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|索引 ID 的符号。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回`SymTagCompilandDetails`(之一[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值)。|

## <a name="remarks"></a>备注
 编译器经常在窗体，称为双步编译器;在某些编译器版本中，每次传递由单独的程序进行处理。 这些参数称为前端和后端编译器，分别，因此后端和前端版本号的符号属性。

## <a name="see-also"></a>请参阅
- [编译单位](../../debugger/debug-interface-access/compiland.md)
- [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)