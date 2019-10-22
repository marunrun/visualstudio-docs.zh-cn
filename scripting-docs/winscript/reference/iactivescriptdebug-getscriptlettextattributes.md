---
title: IActiveScriptDebug：： GetScriptletTextAttributes |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptDebug.GetScriptletTextAttributes
apilocation:
- jscript.dll
helpviewer_keywords:
- IActiveScriptDebug::GetScriptletTextAttributes
ms.assetid: b3990d86-5fdf-4c9f-9678-3f4b808c7ca8
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6a5dd9e219e51b001659225636396fe45ac815b9
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572810"
---
# <a name="iactivescriptdebuggetscriptlettextattributes"></a>IActiveScriptDebug::GetScriptletTextAttributes
返回任意 scriptlet 的文本特性。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetScriptletTextAttributes(  
   LPCOLESTR          pstrCode,  
   ULONG              uNumCodeChars,  
   LPCOLESTR          pstrDelimiter,  
   DWORD              dwFlags,  
   SOURCE_TEXT_ATTR*  pattr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstrCode`  
 中Scriptlet 文本。 此字符串不需要以 null 结尾。  
  
 `uNumCodeChars`  
 中Scriptlet 文本中的字符数。  
  
 `pstrDelimiter`  
 中Scriptlet 分隔符的地址。 当从文本流分析 `pstrCode` 时，主机通常使用分隔符（如两个单引号（' '）来检测 scriptlet 的末尾。 此参数指定主机使用的分隔符，允许脚本引擎提供某些条件基元预处理（例如，用两个单引号替换单引号 ['] 以用作分隔符）。 脚本引擎使用此信息的确切方式取决于脚本引擎。 如果主机未使用分隔符来标记 scriptlet 的末尾，则将此参数设置为 NULL。  
  
 `dwFlags`  
 中与 scriptlet 关联的标志。 可以是这些值的组合：  
  
|返回的常量|“值”|描述|  
|--------------|-----------|-----------------|  
|GETATTRTYPE_DEPSCAN|0x0001|指示应分别用 SOURCETEXT_ATTR_IDENTIFIER 和 SOURCETEXT_ATTR_MEMBERLOOKUP 标志识别标识符和点运算符。|  
|GETATTRFLAG_THIS|0x0100|指示应通过 SOURCETEXT_ATTR_THIS 标志标识当前对象的标识符。|  
|GETATTRFLAG_HUMANTEXT|0x8000|指示应通过 SOURCETEXT_ATTR_HUMANTEXT 标志标识字符串内容和注释文本。|  
  
 `pattr`  
 [in，out]包含返回的属性的缓冲区。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 实现 `IDebugDocumentText` 接口的智能主机可以使用此方法委托对 `IDebugDocumentText::GetText` 方法的调用。  
  
 提供此调用是因为 scriptlet 往往是表达式，并且可能具有与脚本块不同的语法。 如果它们具有相同的语法，此方法的实现将与 `GetScriptTextAttributes` 方法的实现完全相同。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptDebug 接口](../../winscript/reference/iactivescriptdebug-interface.md)   
 [IActiveScriptDebug：： getscripttextattribute](../../winscript/reference/iactivescriptdebug-getscripttextattributes.md)    
 [IDebugDocumentText 接口](../../winscript/reference/idebugdocumenttext-interface.md)   
 [IDebugDocumentText：： GetText](../../winscript/reference/idebugdocumenttext-gettext.md)    
 [SOURCE_TEXT_ATTR 枚举](../../winscript/reference/source-text-attr-enumeration.md)