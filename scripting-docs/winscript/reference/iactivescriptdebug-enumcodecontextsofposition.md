---
title: IActiveScriptDebug::EnumCodeContextsOfPosition | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptDebug.EnumCodeContextsOfPosition
apilocation:
- jscript.dll
helpviewer_keywords:
- IActiveScriptDebug::EnumCodeContextsOfPosition
ms.assetid: 19f44420-bcc8-4c10-8c38-378d96044117
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c364d00941a65272b4d22cc7674a0f0e6178f099
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63009737"
---
# <a name="iactivescriptdebugenumcodecontextsofposition"></a>IActiveScriptDebug::EnumCodeContextsOfPosition
智能主机用于委派`IDebugDocumentContext::EnumCodeContexts`方法。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT EnumCodeContextsOfPosition(  
   DWORD_PTR                 dwSourceContext,  
   ULONG                     uCharacterOffset,  
   ULONG                     uNumChars,  
   IEnumDebugCodeContexts**  ppescc  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwSourceContext`  
 [in]源上下文提供给`IActiveScriptParse::ParseScriptText`或`IActiveScriptParse::AddScriptlet`。  
  
 `uCharacterOffset`  
 [in]字符相对于脚本文本的起始偏移量。  
  
 `uNumChars`  
 [in]在此上下文中的字符数。  
  
 `ppescc`  
 [out]指定范围中的代码上下文枚举器。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 智能主机使用此方法委托`IDebugDocumentContext::EnumCodeContexts`方法。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptDebug 接口](../../winscript/reference/iactivescriptdebug-interface.md)   
 [IDebugDocumentContext::EnumCodeContexts](../../winscript/reference/idebugdocumentcontext-enumcodecontexts.md)