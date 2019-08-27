---
title: 'Idebugdocumenthelper:: Definescriptblock |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHelper.DefineScriptBlock
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentHelper::DefineScriptBlock
ms.assetid: e4120377-f04f-44b1-950b-2beba06c9c12
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2a320e4e43a983ace4decbaa68de0b1a7df7d457
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62783019"
---
# <a name="idebugdocumenthelperdefinescriptblock"></a>IDebugDocumentHelper::DefineScriptBlock
指示特定范围的字符，是由给定的脚本引擎处理的脚本块帮助程序。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT DefineScriptBlock(  
   ULONG           ulCharOffset,  
   ULONG           cChars,  
   IActiveScript*  pas,  
   BOOL            fScriptlet,  
   DWORD_PTR*      pdwSourceContext  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ulCharOffset`  
 [in]脚本块的开始位置。  
  
 `cChars`  
 [in]脚本块中的字符数。  
  
 `pas`  
 [in]此脚本块的脚本引擎。  
  
 `fScriptlet`  
 [in]指示脚本块是否 scriptlet 的标志。  
  
 `pdwSourceContext`  
 [out]脚本块的源上下文。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 智能主机可以使用此方法时其文档包含嵌入式的脚本块。 当其代码包含对其他语言的嵌入式的脚本时，语言引擎可以使用此方法。  
  
 脚本引擎负责进行中的所有语法着色和代码上下文查找脚本块。  
  
 `DefineScriptBlock`添加文本后，应调用方法 (例如，使用`IDebugDocumentHelper::AddDBCSText`方法)，但该脚本之前已分析块 (例如，使用`IActiveScriptParse ::ParseScriptText`方法)。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentHelper 接口](../../winscript/reference/idebugdocumenthelper-interface.md)   
 [IDebugDocumentHelper::AddDBCSText](../../winscript/reference/idebugdocumenthelper-adddbcstext.md)   
 [IDebugDocumentHelper::AddUnicodeText](../../winscript/reference/idebugdocumenthelper-addunicodetext.md)