---
title: IActiveScriptError::GetSourcePosition |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptError.GetSourcePosition
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptError_GetSourcePosition
ms.assetid: ae9b26b1-82a7-4645-9686-3261d8248664
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4446235a9584bc45fad84b6f92ecc02592e554f3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63009619"
---
# <a name="iactivescripterrorgetsourceposition"></a>IActiveScriptError::GetSourcePosition
检索错误发生时脚本引擎已运行脚本的源代码中的位置。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetSourcePosition(  
    DWORD *pdwSourceContext,  // context cookie  
    ULONG *pulLineNumber,     // line number of error  
    LONG *pichCharPosition    // character position of error  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdwSourceContext`  
 [out]接收 cookie 标识上下文变量的地址。 此参数的解释取决于主机应用程序。  
  
 `pulLineNumber`  
 [out]发生错误的源文件中接收的行号的变量的地址。  
  
 `pichCharPosition`  
 [out]一个变量来接收错误发生位置的行中的字符位置的地址。  
  
## <a name="return-value"></a>返回值  
 返回`S_OK`如果成功，或`E_FAIL`如果检索不到该位置。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptError](../../winscript/reference/iactivescripterror.md)