---
title: IActiveScriptAuthor::GetScriptletTextAttributes |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetScriptletTextAttributes
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetScriptletTextAttributes
ms.assetid: 082edfce-6c5b-4e5e-b942-31b423a4fa1d
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cb8f1b5aac6df8d8659fa323f3f1efcb7721d97f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955052"
---
# <a name="iactivescriptauthorgetscriptlettextattributes"></a>IActiveScriptAuthor::GetScriptletTextAttributes
返回 scriptlet 文本的属性。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetScriptletTextAttributes(  
   LPCOLESTR pszCode,  
   ULONG cch,  
   LPCOLESTR pszDelimiter,  
   DWORD dwFlags,  
   SOURCE_TEXT_ATTR *pattr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszCode`  
 [在中，size_is (`cch`)] 的 scriptlet 文本。 此字符串没有以 null 结束。  
  
 `cch`  
 [in]用于的大小`pszCode`和`pattr`参数。  
  
 `pszDelimiter`  
 [in]结束 scriptlet 分隔符的地址。 当`pszCode`进行分析的文本流，从主机通常使用分隔符 （如两个单引号），来检测 scriptlet 的末尾。 如果没有分隔符用于标识 scriptlet 的末尾，此参数设置为 NULL。  
  
 `dwFlags`  
 [in]与 scriptlet 文本属性相关联的标志。 可以是以下值的组合。  
  
|返回的常量|“值”|描述|  
|--------------|-----------|-----------------|  
|GETATTRTYPE_DEPSCAN|0x0001|标识具有 SOURCETEXT_ATTR_IDENTIFIER 属性的标识符和标识具有 SOURCETEXT_ATTR_MEMBERLOOKUP 属性的圆点运算符。|  
|GETATTRFLAG_THIS|0x0100|标识具有 SOURCETEXT_ATTR_THIS 属性的当前对象。|  
|GETATTRFLAG_HUMANTEXT|0x8000|标识具有 SOURCETEXT_ATTR_HUMANTEXT 属性的字符串内容和注释文本。|  
  
 `pattr`  
 [in、 out size_is (`cch`)] 的 scriptlet 代码的颜色信息。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)   
 [IActiveScriptAuthor::GetScriptTextAttributes](../../winscript/reference/iactivescriptauthor-getscripttextattributes.md)   
 [SOURCE_TEXT_ATTR 枚举](../../winscript/reference/source-text-attr-enumeration.md)