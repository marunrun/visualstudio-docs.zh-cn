---
title: IActiveScriptAuthor：： Getscripttextattribute |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetScriptTextAttributes
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetScriptTextAttributes
ms.assetid: a53451de-cc5c-4b53-8e5f-81e196364caf
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f89c7b654cc2ac7248598ee6498a3a290d17e2ef
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72563148"
---
# <a name="iactivescriptauthorgetscripttextattributes"></a>IActiveScriptAuthor::GetScriptTextAttributes
返回脚本块的文本特性。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetScriptTextAttributes(  
    LPCOLESTR        pszCode,  
    ULONG            cch,  
    LPCOLESTR        pszDelimiter,  
    DWORD            dwFlags,  
    SOURCE_TEXT_ATTR *pattr);  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszCode`  
 [in，size_is （`cch`）]脚本块的文本。 此字符串不一定要终止 null。  
  
 `cch`  
 中用于 `pszCode` 和 `pattr` 参数的大小。  
  
 `pszDelimiter`  
 中脚本结束分隔符的地址。 当从文本流分析 `pszCode` 时，主机通常使用分隔符（如两个单引号）来检测 scriptlet 的末尾。 如果没有分隔符用于标识脚本块的末尾，则将此参数设置为 NULL。  
  
 `dwFlags`  
 中与脚本块的文本特性相关联的标志。 可以是以下值的组合：  
  
|常量|值|说明|  
|--------------|-----------|-----------------|  
|GETATTRTYPE_DEPSCAN|0x0001|标识具有 SOURCETEXT_ATTR_IDENTIFIER 特性的标识符，并标识具有 SOURCETEXT_ATTR_MEMBERLOOKUP 属性的点运算符。|  
|GETATTRFLAG_THIS|0x0100|标识具有 SOURCETEXT_ATTR_THIS 特性的当前对象。|  
|GETATTRFLAG_HUMANTEXT|0x8000|标识具有 SOURCETEXT_ATTR_HUMANTEXT 属性的字符串内容和注释文本。|  
  
 `pattr`  
 [in，out，size_is （`cch`）]脚本块代码的颜色信息。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)   
 [SOURCE_TEXT_ATTR 枚举](../../winscript/reference/source-text-attr-enumeration.md)