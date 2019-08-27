---
title: IActiveScriptError::GetExceptionInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptError.GetExceptionInfo
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptError_GetExceptionInfo
ms.assetid: 528416cc-8468-4ad7-a6c2-fa1daf6ecf33
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 71e8f787e6837e6fa41c7b3cd831448b5d20a95e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63009566"
---
# <a name="iactivescripterrorgetexceptioninfo"></a>IActiveScriptError::GetExceptionInfo
检索有关脚本引擎运行脚本时发生错误的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetExceptionInfo(  
    EXCEPINFO *pexcepinfo  // structure for exception information  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pexcepinfo`  
 [out]地址`EXCEPINFO`接收错误的信息的结构。  
  
## <a name="return-value"></a>返回值  
 返回`S_OK`如果成功，或`E_FAIL`是否发生错误。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptError](../../winscript/reference/iactivescripterror.md)