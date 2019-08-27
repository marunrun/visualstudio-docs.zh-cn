---
title: IDebugStackFrame::GetLanguageString |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugStackFrame.GetLanguageString
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugStackFrame::GetLanguageString
ms.assetid: 561d6306-f214-422f-abc9-b502cbfbe208
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cab0c0ab317754305ca2440748dd680e31750d8a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62934663"
---
# <a name="idebugstackframegetlanguagestring"></a>IDebugStackFrame::GetLanguageString
返回语言的短或长文本描述。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetLanguageString(  
   BOOL   fLong,  
   BSTR*  pbstrLanguage  
);  
```  
  
#### <a name="parameters"></a>参数  
 `fLong`  
 [in]标志，其中`TRUE`返回的详细说明和`FALSE`返回的简短说明。  
  
 `pbstrLanguage`  
 [out]语言的描述。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 通常情况下，如果`fLong`是`FALSE`，此方法提供仅与堆栈帧关联的语言的名称。 当`fLong`是`TRUE`，此方法可能会提供完整的产品说明。  
  
## <a name="see-also"></a>请参阅  
 [IDebugStackFrame 接口](../../winscript/reference/idebugstackframe-interface.md)