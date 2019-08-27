---
title: IActiveScriptDebug::GetScriptTextAttributes | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptDebug.GetScriptTextAttributes
apilocation:
- jscript.dll
helpviewer_keywords:
- IActiveScriptDebug::GetScriptTextAttributes
ms.assetid: 2e8bda34-db0c-4b2e-a17f-82c4e0dbbc8c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: faec7cf65bed39a038c5ab7cc09d9908063a2c63
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63009540"
---
# <a name="iactivescriptdebuggetscripttextattributes"></a>IActiveScriptDebug::GetScriptTextAttributes
返回脚本文本的任意块的文本属性。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetScriptTextAttributes(  
   LPCOLESTR          pstrCode,  
   ULONG              uNumCodeChars,  
   LPCOLESTR          pstrDelimiter,  
   DWORD              dwFlags,  
   SOURCE_TEXT_ATTR*  pattr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstrCode`  
 [in]脚本块文本。 此字符串不需要终止 null。  
  
 `uNumCodeChars`  
 [in]脚本块文本中的字符数。  
  
 `pstrDelimiter`  
 [in]最终的脚本块分隔符的地址。 当`pstrCode`进行分析的文本流，从主机通常使用分隔符，如两个单引号 （'），以检测脚本块的末尾。 此参数指定主机使用，允许脚本引擎来提供某些条件的原始预处理的分隔符 （例如，与使用用作分隔符的两个单引号替换单引号 [']）。 完全如何 （以及是否） 脚本的引擎使用此信息取决于脚本引擎。 如果主机不使用分隔符来标记的脚本块的结尾，此参数设置为 NULL。  
  
 `dwFlags`  
 [in]与脚本块关联的标志。 可以是这些值的组合：  
  
|返回的常量|“值”|描述|  
|--------------|-----------|-----------------|  
|GETATTRTYPE_DEPSCAN|0x0001|指示标识符和点运算符应进行标识与 SOURCETEXT_ATTR_IDENTIFIER 和 SOURCETEXT_ATTR_MEMBERLOOKUP 标志，分别。|  
|GETATTRFLAG_THIS|0x0100|指示当前对象的标识符应使用 SOURCETEXT_ATTR_THIS 标志来标识。|  
|GETATTRFLAG_HUMANTEXT|0x8000|指示字符串内容和注释文本应使用 SOURCETEXT_ATTR_HUMANTEXT 标志来标识。|  
  
 `pattr`  
 [in、 out]要包含返回的特性的缓冲区。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 实现智能主机`IDebugDocumentText`接口可以使用此方法委托调用`IDebugDocumentText::GetText`方法。  
  
 对脚本块; 此方法`GetScriptletTextAttributes`方式适用于的 scriptlet。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptDebug 接口](../../winscript/reference/iactivescriptdebug-interface.md)   
 [IActiveScriptDebug::GetScriptletTextAttributes](../../winscript/reference/iactivescriptdebug-getscriptlettextattributes.md)   
 [IDebugDocumentText 接口](../../winscript/reference/idebugdocumenttext-interface.md)   
 [IDebugDocumentText::GetText](../../winscript/reference/idebugdocumenttext-gettext.md)   
 [SOURCE_TEXT_ATTR 枚举](../../winscript/reference/source-text-attr-enumeration.md)