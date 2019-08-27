---
title: IDebugCookie::SetDebugCookie |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugCookie.SetDebugCookie
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugCookie::SetDebugCookie
ms.assetid: 9cba3b05-ff81-4fb0-9382-e9338cb9192d
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c83c1331a95e48afa02b0b37557ca5bd042261d7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62974470"
---
# <a name="idebugcookiesetdebugcookie"></a>IDebugCookie::SetDebugCookie
设置调试应用程序 cookie。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetDebugCookie(  
   DWORD  dwDebugAppCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwDebugAppCookie`  
 [in]一个标识的调试应用程序的 cookie。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法设置调试应用程序 cookie，从而允许多个调试器附加到进程。  
  
## <a name="see-also"></a>请参阅  
 [IDebugCookie 接口](../../winscript/reference/idebugcookie-interface.md)