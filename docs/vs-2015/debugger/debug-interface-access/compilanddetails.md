---
title: CompilandDetails |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CompilandDetails symbol
ms.assetid: ddc7d794-c622-4c63-b2a6-72f8b2d0022a
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 34349bf096d8bb98ae4b3de7c7a922b8d28bc4f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65703002"
---
# <a name="compilanddetails"></a>CompilandDetails
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

编译单位信息在带有 `SymTagCompiland` 标记 () 的符号和 `SymTagCompilandDetails` (详细) 详细信息的标记之间拆分。 `SymTagCompilandDetails` 需要加载其他符号。 不过，它提供了有关符号不提供的编译单位的丰富信息 `SymTagCompiland` 。  
  
## <a name="properties"></a>属性  
 下表显示了对此符号类型有效的属性。  
  
|属性|数据类型|说明|  
|--------------|---------------|-----------------|  
|[IDiaSymbol::get_backEndBuild](../../debugger/debug-interface-access/idiasymbol-get-backendbuild.md)|`DWORD`|编译器的后端内部版本号。|  
|[IDiaSymbol::get_backEndMajor](../../debugger/debug-interface-access/idiasymbol-get-backendmajor.md)|`DWORD`|编译器的后端主版本号。|  
|[IDiaSymbol::get_backEndMinor](../../debugger/debug-interface-access/idiasymbol-get-backendminor.md)|`DWORD`|编译器的后端次版本号。|  
|[IDiaSymbol::get_compilerName](../../debugger/debug-interface-access/idiasymbol-get-compilername.md)|`BSTR`|生成此编译单位的编译器的名称仅在 DIA SDK v2.0 或更高版本) 中 (。|  
|[IDiaSymbol::get_editAndContinueEnabled](../../debugger/debug-interface-access/idiasymbol-get-editandcontinueenabled.md)|`BOOL`|`TRUE` 如果在编译时启用了 "编辑并继续"。|  
|[IDiaSymbol::get_frontEndBuild](../../debugger/debug-interface-access/idiasymbol-get-frontendbuild.md)|`DWORD`|编译器的前端内部版本号。|  
|[IDiaSymbol::get_frontEndMajor](../../debugger/debug-interface-access/idiasymbol-get-frontendmajor.md)|`DWORD`|编译器的前端主版本号。|  
|[IDiaSymbol::get_frontEndMinor](../../debugger/debug-interface-access/idiasymbol-get-frontendminor.md)|`DWORD`|编译器的前端次版本号。|  
|[IDiaSymbol::get_hasDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-hasdebuginfo.md)|`BOOL`|`TRUE` 如果此编译单位具有调试信息 (仅 DIA SDK v2.0 或更高版本) 。|  
|[IDiaSymbol::get_hasManagedCode](../../debugger/debug-interface-access/idiasymbol-get-hasmanagedcode.md)|`BOOL`|`TRUE` 如果此编译单位包含托管代码 (仅在 DIA SDK v2.0 或更高版本) 中。|  
|[IDiaSymbol::get_hasSecurityChecks](../../debugger/debug-interface-access/idiasymbol-get-hassecuritychecks.md)|`BOOL`|`TRUE` 如果编译单位是用 [/gs (Buffer 安全检查 ](https://msdn.microsoft.com/library/8d8a5ea1-cd5e-42e1-bc36-66e1cd7e731e) 编译的) 编译器交换机 (仅在 DIA SDK v2.0 或更高) 版本中进行。|  
|[IDiaSymbol::get_isCVTCIL](../../debugger/debug-interface-access/idiasymbol-get-iscvtcil.md)|`BOOL`|`TRUE` 如果编译单位已从公共中间语言 (CIL) 代码转换为本机代码。|  
|[IDiaSymbol::get_isDataAligned](../../debugger/debug-interface-access/idiasymbol-get-isdataaligned.md)|`BOOL`|`TRUE` 如果 (UDT) 的用户定义类型已与某些指定的内存边界对齐， (只在 DIA SDK 8.0 或更高) 版本中使用。|  
|[IDiaSymbol::get_isHotpatchable](../../debugger/debug-interface-access/idiasymbol-get-ishotpatchable.md)|`BOOL`|`TRUE` 如果编译单位是用/hotpatch 编译的 (仅在 DIA SDK v2.0 或更高) 版本中 ([创建可热修补映像) ](https://msdn.microsoft.com/library/aad539b6-c053-4c78-8682-853d98327798) 编译器开关。|  
|[IDiaSymbol::get_isLTCG](../../debugger/debug-interface-access/idiasymbol-get-isltcg.md)|`BOOL`|`TRUE` 如果编译单位是用 [/ltcg (链接时代码生成 ](https://msdn.microsoft.com/library/788c6f52-fdb8-40c2-90af-4026ea2cf2e2) 编译的) 编译器交换机 (只在 DIA SDK v2.0 或更高) 版本中进行。|  
|[IDiaSymbol::get_isMSILNetmodule](../../debugger/debug-interface-access/idiasymbol-get-ismsilnetmodule.md)|`BOOL`|如果编译单位是 Microsoft 中间语言 (MSIL) 模块仅在 DIA SDK 8.0 或更高) 版本中 (，则为 TRUE。|  
|[IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)|`DWORD`|源代码语言。|  
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|编译单位的符号。|  
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|  
|[IDiaSymbol::get_platform](../../debugger/debug-interface-access/idiasymbol-get-platform.md)|`DWORD`|编译编译单位的平台 () 的 [CV_CPU_TYPE_e 枚举](../../debugger/debug-interface-access/cv-cpu-type-e.md) 值之一。|  
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|符号的索引 ID。|  
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回 `SymTagCompilandDetails` () 的 [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md) 值之一。|  
  
## <a name="remarks"></a>备注  
 编译器通常以称为两遍编译器的形式提供;在某些编译器版本中，每个传递都由单独的程序处理。 它们分别称为前端和后端编译器，因此是后端版本号和前端版本号的符号属性。  
  
## <a name="see-also"></a>另请参阅  
 [编译单位](../../debugger/debug-interface-access/compiland.md)   
 [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
