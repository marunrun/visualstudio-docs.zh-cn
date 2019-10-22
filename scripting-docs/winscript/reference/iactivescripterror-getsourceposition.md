---
title: IActiveScriptError：： GetSourcePosition |Microsoft Docs
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
ms.openlocfilehash: 76ed307f988a3e5bf77ff978c466eda6e5dfee18
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576885"
---
# <a name="iactivescripterrorgetsourceposition"></a>IActiveScriptError::GetSourcePosition
检索源代码中脚本引擎运行脚本时出错的位置。  
  
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
 弄一个变量的地址，该变量接收标识上下文的 cookie。 此参数的解释取决于主机应用程序。  
  
 `pulLineNumber`  
 弄一个变量的地址，该变量接收发生错误的源文件中的行号。  
  
 `pichCharPosition`  
 弄一个变量的地址，该变量接收发生错误的行中的字符位置。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`; 如果未检索到位置，则返回 `E_FAIL`。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptError](../../winscript/reference/iactivescripterror.md)