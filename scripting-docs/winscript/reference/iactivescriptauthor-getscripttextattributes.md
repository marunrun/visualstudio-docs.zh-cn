---
title: IActiveScriptAuthor::GetScriptTextAttributes |Microsoft Docs
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
ms.openlocfilehash: 75e0d5edf7cf2f83e814036cec56a1b19a89813e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955115"
---
# <a name="iactivescriptauthorgetscripttextattributes"></a>IActiveScriptAuthor::GetScriptTextAttributes
返回脚本块的文本属性。  
  
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
 [在中，size_is (`cch`)] 的脚本块的文本。 此字符串没有以 null 结束。  
  
 `cch`  
 [in]用于的大小`pszCode`和`pattr`参数。  
  
 `pszDelimiter`  
 [in]脚本结束分隔符的地址。 当`pszCode`进行分析的文本流，从主机通常使用分隔符 （如两个单引号），来检测 scriptlet 的末尾。 如果没有定界符来标识脚本块的末尾，此参数设置为 NULL。  
  
 `dwFlags`  
 [in]与脚本块的文本属性相关联的标志。 可以是以下值的组合：  
  
|返回的常量|“值”|描述|  
|--------------|-----------|-----------------|  
|GETATTRTYPE_DEPSCAN|0x0001|标识具有 SOURCETEXT_ATTR_IDENTIFIER 属性的标识符和标识具有 SOURCETEXT_ATTR_MEMBERLOOKUP 属性的圆点运算符。|  
|GETATTRFLAG_THIS|0x0100|标识具有 SOURCETEXT_ATTR_THIS 属性的当前对象。|  
|GETATTRFLAG_HUMANTEXT|0x8000|标识具有 SOURCETEXT_ATTR_HUMANTEXT 属性的字符串内容和注释文本。|  
  
 `pattr`  
 [in、 out size_is (`cch`)] 的脚本块代码的颜色信息。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)   
 [SOURCE_TEXT_ATTR 枚举](../../winscript/reference/source-text-attr-enumeration.md)