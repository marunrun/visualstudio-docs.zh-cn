---
title: IMachineDebugManagerCookie::AddApplication |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IMachineDebugManagerCookie.AddApplication
apilocation:
- scrobj.dll
helpviewer_keywords:
- IMachineDebugManagerCookie::AddApplication
ms.assetid: 4d5503c5-aca9-4cf7-9900-f77bf5f3263d
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c71983dd5f1273679351bc45c1db2df62757d153
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977651"
---
# <a name="imachinedebugmanagercookieaddapplication"></a>IMachineDebugManagerCookie::AddApplication
将添加到正在运行的应用程序的应用程序列表。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT AddApplication(  
   IRemoteDebugApplication*  pda,  
   DWORD                     dwDebugAppCookie,  
   DWORD*                    pdwAppCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pda`  
 [in]为正在运行的应用程序的应用程序列表。  
  
 `dwDebugAppCookie`  
 [in]一个标识的调试应用程序的 cookie。  
  
 `pdwAppCookie`  
 [out]一个用于从计算机调试管理器删除应用程序的 cookie。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 进程调试管理器调用此方法时`IProcessDebugManager::AddApplication`调用。  
  
## <a name="see-also"></a>请参阅  
 [IMachineDebugManagerCookie Interface](../../winscript/reference/imachinedebugmanagercookie-interface.md)   
 [IMachineDebugManagerCookie::RemoveApplication](../../winscript/reference/imachinedebugmanagercookie-removeapplication.md)   
 [IProcessDebugManager::AddApplication](../../winscript/reference/iprocessdebugmanager-addapplication.md)