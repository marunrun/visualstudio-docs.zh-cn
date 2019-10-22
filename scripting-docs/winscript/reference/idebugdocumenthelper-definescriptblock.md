---
title: IDebugDocumentHelper：:D efineScriptBlock |Microsoft Docs
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
ms.openlocfilehash: 6a2418b18e80ac86b672b3847f24ef9084ed1252
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576979"
---
# <a name="idebugdocumenthelperdefinescriptblock"></a>IDebugDocumentHelper::DefineScriptBlock
向帮助器指示特定范围的字符是由给定脚本引擎处理的脚本块。  
  
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
 中脚本块的开始位置。  
  
 `cChars`  
 中脚本块中的字符数。  
  
 `pas`  
 中此脚本块的脚本引擎。  
  
 `fScriptlet`  
 中指示脚本块是否为 scriptlet 的标志。  
  
 `pdwSourceContext`  
 弄脚本块的源上下文。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 当智能主机的文档包含嵌入的脚本块时，可以使用此方法。 当语言引擎的代码包含用于其他语言的嵌入脚本时，它可以使用此方法。  
  
 脚本引擎负责脚本块中的所有语法着色和代码上下文查找。  
  
 在添加文本（例如，使用 `IDebugDocumentHelper::AddDBCSText` 方法）之后但在分析脚本块之前，应调用 `DefineScriptBlock` 方法（例如，使用 `IActiveScriptParse ::ParseScriptText` 方法）。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentHelper 接口](../../winscript/reference/idebugdocumenthelper-interface.md)   
 [IDebugDocumentHelper：： AddDBCSText](../../winscript/reference/idebugdocumenthelper-adddbcstext.md)    
 [IDebugDocumentHelper::AddUnicodeText](../../winscript/reference/idebugdocumenthelper-addunicodetext.md)