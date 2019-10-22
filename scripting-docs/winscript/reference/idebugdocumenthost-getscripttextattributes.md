---
title: IDebugDocumentHost：： Getscripttextattribute |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHost.GetScriptTextAttributes
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugDocumentHost::GetScriptTextAttributes
ms.assetid: fe459d0d-937f-4176-be81-99d5cca121a1
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3b18f4f49fa157b78e4f1fd6c7766e929890a6c6
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72569199"
---
# <a name="idebugdocumenthostgetscripttextattributes"></a>IDebugDocumentHost::GetScriptTextAttributes
返回文档文本块的文本特性。  
  
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
 中脚本块文本。 此字符串不需要以 null 值终止。  
  
 `uNumCodeChars`  
 中脚本块文本中的字符数。  
  
 `pstrDelimiter`  
 中脚本结束分隔符的地址。 当从文本流分析 `pstrCode` 时，主机通常使用分隔符（如两个单引号（' '）来检测脚本块的结尾。 此参数指定主机使用的分隔符，允许脚本引擎提供某些条件基元预处理（例如，用两个单引号替换单引号 ['] 以用作分隔符）。 脚本引擎使用此信息的确切方式取决于脚本引擎。 如果主机未使用分隔符来标记脚本块的末尾，则将此参数设置为 NULL。  
  
 `dwFlags`  
 中与脚本块关联的标志。 可以是这些值的组合：  
  
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
|`E_NOTIMPL`|该主机仅使用默认属性。|  
  
## <a name="remarks"></a>备注  
 此方法返回任意文档文本块的文本特性。 主机可以 `E_NOTIMPL` 返回，在这种情况下，将使用默认属性。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentHost 接口](../../winscript/reference/idebugdocumenthost-interface.md)   
 [SOURCE_TEXT_ATTR 枚举](../../winscript/reference/source-text-attr-enumeration.md)