---
title: IDebugCodeContext::GetDocumentContext |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugCodeContext.GetDocumentContext
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugCodeContext::GetDocumentContext
ms.assetid: 9fe17b65-3a8c-4d21-9b66-0e4ff303af72
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 48c707432ddb94fae111c971b89c8ff74f34ac21
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62974535"
---
# <a name="idebugcodecontextgetdocumentcontext"></a>IDebugCodeContext::GetDocumentContext
返回与此代码的上下文关联的文档上下文。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetDocumentContext(  
   IDebugDocumentContext**  ppsc  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppsc`  
 [out]与此代码的上下文关联的文档上下文。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 用于文本文档的字符位置范围应包括整个语句的文本。 这使调试器 IDE 以突出显示当前的源语句。  
  
## <a name="see-also"></a>请参阅  
 [IDebugCodeContext 接口](../../winscript/reference/idebugcodecontext-interface.md)