---
title: IActiveScriptSiteDebug::GetDocumentContextFromPosition |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSiteDebug.GetDocumentContextFromPosition
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSiteDebug::GetDocumentContextFromPosition
ms.assetid: ba5f7348-0107-4b12-b949-79a012476cf7
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: df6c59fea5cfd60b6ae9a1b34e7000bd38dd9920
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992549"
---
# <a name="iactivescriptsitedebuggetdocumentcontextfromposition"></a>IActiveScriptSiteDebug::GetDocumentContextFromPosition
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
 [IActiveScriptSiteDebug 接口](../../winscript/reference/iactivescriptsitedebug-interface.md)