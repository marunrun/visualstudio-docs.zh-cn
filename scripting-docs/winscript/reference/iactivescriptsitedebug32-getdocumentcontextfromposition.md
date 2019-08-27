---
title: IActiveScriptSiteDebug32::GetDocumentContextFromPosition |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 53348dff-35a6-4303-b263-90c10af06bf3
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 9a52abcfa4defb49526f944469c95a2247f5d85c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992516"
---
# <a name="iactivescriptsitedebug32getdocumentcontextfromposition"></a>IActiveScriptSiteDebug32::GetDocumentContextFromPosition
语言引擎用于委派`IDebugCodeContext::GetSourceContext`。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetDocumentContextFromPosition(  
   DWORD_PTR                dwSourceContext,  
   ULONG                    uCharacterOffset,  
   ULONG                    uNumChars,  
   IDebugDocumentContext**  ppsc  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwSourceContext`  
 [in]源内容提供给`ParseScriptText`或`AddScriptlet`。  
  
 `uCharacterOffset`  
 [in]字符相对于脚本块或 scriptlet 的起始偏移量。  
  
 `uNumChars`  
 [in]在此上下文中的字符数。  
  
 `ppsc`  
 [out]文档上下文对应于此字符位置范围。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 语言引擎使用此方法委托`IDebugCodeContext::GetSourceContext`。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSiteDebug32 接口](../../winscript/reference/iactivescriptsitedebug32-interface.md)